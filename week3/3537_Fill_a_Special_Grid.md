# [3537] [Fill_a_Special_Grid]

## Code (C++)

```cpp
class Solution {
public:
    vector<vector<int>> specialGrid(int n) {
        int size = 1 << n;
        vector<vector<int>> ans(size, vector<int>(size, 0));
        auto fill = [&](auto& self, int r, int c, int len, int offset) -> void {
            if (len == 1) {
                ans[r][c] = offset;
                return;
            }
            int half = len / 2;
            int step = half * half;
            
            self(self, r, c + half, half, offset);                  // Top-Right
            self(self, r + half, c + half, half, offset + step);    // Bottom-Right
            self(self, r + half, c, half, offset + 2 * step);       // Bottom-Left
            self(self, r, c, half, offset + 3 * step);              // Top-Left
        };
        fill(fill, 0, 0, size, 0);
        return ans;
    }
};
```
## Acceptance Screen Shot
![alt text](image.png)