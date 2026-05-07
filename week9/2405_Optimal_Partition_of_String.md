
## Code (C++)

```cpp
class Solution {
public:
    int partitionString(string s) {
        int res = 1, mask = 0;
        for (char c : s) {
            int val = c - 'a';
            if (mask & (1 << val)) {
                res++;
                mask = 0;
            }
            mask |= (1 << val);
        }
        return res;
    }
};
```
## Acceptance Screen Shot
![alt text](2366_Minimum_Replacements_to_Sort_the_Array.png)