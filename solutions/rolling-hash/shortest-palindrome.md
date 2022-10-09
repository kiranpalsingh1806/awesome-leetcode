## Heading here

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    string shortestPalindrome(string s) {
        unsigned d = 16777619, h = 0, rh = 0, p = 1, maxLen = 0;
        for (int i = 0; i < s.size(); ++i) {
            h = h * d + s[i] - 'a';
            rh += (s[i] - 'a') * p;
            p *= d;
            if (h == rh) maxLen = i + 1;
        }
        return string(rbegin(s), rbegin(s) + s.size() - maxLen) + s;
    }
};
```

</details>