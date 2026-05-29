
## Code (C++)

```cpp
class Solution {
public:
    int dp[100][100][100];

    int removeBoxes(vector<int>& boxes) {
        memset(dp, 0, sizeof(dp));
        return solve(boxes, 0, (int)boxes.size()-1, 0);
    }

    // dp[l][r][k] = max points from boxes[l..r] with k extra boxes
    //               of the same color as boxes[l] attached on the left
    int solve(vector<int>& boxes, int l, int r, int k) {
        if (l > r) return 0;
        if (dp[l][r][k]) return dp[l][r][k];

        // Option 1: remove the k+1 copies of boxes[l] color immediately
        int res = (k+1)*(k+1) + solve(boxes, l+1, r, 0);

        // Option 2: find some m where boxes[m] == boxes[l], defer removal
        for (int m = l+1; m <= r; m++) {
            if (boxes[m] == boxes[l]) {
                res = max(res, solve(boxes, l+1, m-1, 0) + solve(boxes, m, r, k+1));
            }
        }
        return dp[l][r][k] = res;
    }
};
```
## Acceptance Screen Shot
![alt text](546_Remove_Boxes.png)