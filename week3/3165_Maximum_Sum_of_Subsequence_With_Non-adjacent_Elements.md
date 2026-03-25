# [3165] [Maximum_Sum_of_Subsequence_With_Non-adjacent_Elements]

## Code (C++)

```cpp
class Solution {
    struct Node {
        long long v00, v01, v10, v11;
    };
    vector<Node> tree;
    long long MOD = 1e9 + 7;
    void build(int node, int start, int end, vector<int>& nums) {
        if (start == end) {
            tree[node] = {0, 0, 0, max(0LL, (long long)nums[start])};
            return;
        }
        int mid = (start + end) / 2;
        build(2 * node, start, mid, nums);
        build(2 * node + 1, mid + 1, end, nums);
        pushUp(node);
    }
    void pushUp(int node) {
        auto& L = tree[2 * node];
        auto& R = tree[2 * node + 1];
        tree[node].v00 = max(L.v00 + R.v10, L.v01 + R.v00);
        tree[node].v01 = max(L.v00 + R.v11, L.v01 + R.v01);
        tree[node].v10 = max(L.v10 + R.v10, L.v11 + R.v00);
        tree[node].v11 = max(L.v10 + R.v11, L.v11 + R.v01);
    }
    void update(int node, int start, int end, int idx, int val) {
        if (start == end) {
            tree[node] = {0, 0, 0, max(0LL, (long long)val)};
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(2 * node, start, mid, idx, val);
        else update(2 * node + 1, mid + 1, end, idx, val);
        pushUp(node);
    }
public:
    int maximumSumSubsequence(vector<int>& nums, vector<vector<int>>& queries) {
        int n = nums.size();
        tree.resize(4 * n);
        build(1, 0, n - 1, nums);
        long long ans = 0;
        for (auto& q : queries) {
            update(1, 0, n - 1, q[0], q[1]);
            ans = (ans + max({tree[1].v00, tree[1].v01, tree[1].v10, tree[1].v11})) % MOD;
        }
        return ans;
    }
};
```
## Acceptance Screen Shot
![alt text](image.png)