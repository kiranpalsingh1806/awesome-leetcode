## 1. Count Number of Homogenous Substrings

```cpp
class Solution {
public:
    int countHomogenous(string s) {
        int ans = 1;
        int currentString = 1;
        int MOD = 1e9 + 7;

        for (int i = 1; i < s.length(); i++) {
            if (s[i] == s[i - 1]) {
                currentString++;
            } else {
                currentString = 1;
            }

            ans = (ans + currentString) % MOD;
        }

        return ans;
    }
};
```

## 2. Number of Substrings With Only 1s

```cpp
class Solution {
public:
    int numSub(string s) {
        int ans = 0, MOD = 1e9 + 7;
        int oneCount = 0;

        for (int i = 0; i < s.length(); i++) {
            if (s[i] == '1') {
                oneCount++;
            } else {
                oneCount = 0;
            }
            ans = (ans + oneCount) % MOD;
        }
        return ans;
    }
};
```
