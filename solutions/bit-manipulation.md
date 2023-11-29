- [Bit Manipulation](#bit-manipulation)
  - [17. Number of One bits](#17-number-of-one-bits)

# Bit Manipulation

## 17. Number of One bits

```cpp
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans = 0;

        while(n) {
            n = n & (n - 1);
            ans++;
        }

        return ans;
    }
};
```
