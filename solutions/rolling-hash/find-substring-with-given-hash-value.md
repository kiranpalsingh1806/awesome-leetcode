## Find Substring With Given Hash Value

```cpp
class Solution {
public:
    string subStrHash(string s, int p, int M, int k, int target) {
        
        long h = 0, pp = 1;
        int N = s.size();
        vector<long> hash(N);
        
        string r(rbegin(s), rend(s));
        
        for (int i = 0 ; i < N; i++) {
            h = (h * p + (r[i] - 'a' + 1)) % M;
            
            if (i < k) {
                pp = (pp * p) % M;
            } else {
                h = (h - (r[i - k] - 'a' + 1) * pp % M + M) % M;
            }
            
            if (i >= k - 1) {
                hash[i] = h;
            }
        }
        
        reverse(hash.begin(), hash.end());
        
        for (int i = 0; i < N; i++) {
            if (hash[i] == target) {
                return s.substr(i, k);
            }
        }
        
        return "";
    }
};
```