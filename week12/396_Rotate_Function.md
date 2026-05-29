
## Code (C++)

```cpp
class Solution {
public:
    int maxRotateFunction(vector<int>& nums) {
        int n = nums.size();
        long sum = accumulate(nums.begin(), nums.end(), 0L);
        long f = 0;
        for (int i = 0; i < n; i++) f += (long)i * nums[i];
        long res = f;
        // F(k) = F(k-1) + sum - n * nums[n-k]
        for (int k = 1; k < n; k++) {
            f += sum - (long)n * nums[n-k];
            res = max(res, f);
        }
        return (int)res;
    }
};
```
## Acceptance Screen Shot
![alt text](396_Rotate_Function.png)