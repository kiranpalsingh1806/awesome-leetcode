## Distinct Echo Substrings

```cpp
class Solution {
public:
    int distinctEchoSubstrings(string s) {
        
        int M = 1e8 + 7, cnt = 0;
        int N = s.length();
        vector<int> hash(N);
        
        for (int len = 1; len <= N / 2; len++) {
            
            long h = s[0] - 'a', p = 1;
            unordered_set<string> visited;
            
            for (int i = 1; i < N; i++) {
                if (i < len) {
                    h = (h * 26 + s[i] - 'a') % M; 
                    p = (p * 26) % M;
                } else {
                    h = ((h - (s[i - len] - 'a') * p) * 26 + s[i] - 'a') % M;
                    if (h < 0) h += M;
                    
                    if ( i - 2 * len + 1 >= 0 && hash[i - len] == h) {
                        auto a = s.substr(i - 2 * len + 1, len);
                        
                        if (visited.count(a)) continue;
                        visited.insert(a);
                        
                        if (a == s.substr(i - len + 1, len)) cnt++;
                    }
                }
                hash[i] = h;
            }
        }
        
        return cnt;
    }
};
```