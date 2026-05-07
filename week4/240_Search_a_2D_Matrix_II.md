# [240] [Search_a_2D_Matrix_II]

## Code (C++)

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty() || matrix[0].empty()) return false;
        
        int m = matrix.size();
        int n = matrix[0].size();
        
        // 從右上角開始搜尋
        int row = 0;
        int col = n - 1;
        
        while (row < m && col >= 0) {
            if (matrix[row][col] == target) {
                return true; // 找到目標值
            } else if (matrix[row][col] > target) {
                // 當前值太大，目標一定在左邊，排除當前行
                col--;
            } else {
                // 當前值太小，目標一定在下面，排除當前列
                row++;
            }
        }
        
        return false; // 搜尋完畢仍未找到
    }
};
```
## Acceptance Screen Shot
![alt text](240_Search_a_2D_Matrix_II.png)
