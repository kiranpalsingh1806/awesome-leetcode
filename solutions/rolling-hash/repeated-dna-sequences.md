## Heading here

<details>
<summary> View Code </summary>

```cpp
vector<string> findRepeatedDnaSequences(string s) {
    int N = s.size();
    unordered_map<long long,int> hash;
    vector<string> ans;
    
    if (N <= 10) return ans;
    long long p = 5, h = 0, M = 1e9 + 7, d = 1;
    
    for (int i = N - 1; i >= 0; i--) {
        h = (h * p) % M + (s[i] - 'A' + 1) % M;
        
        if (i + 10 >= N) {
            d = (d * p)  % M;
        } else {
            h = (h - ((s[i + 10] - 'A' + 1) * d) % M + M) % M;
        }
        
        if (hash.find(h) != hash.end() && hash[h] == 1) {
            ans.push_back(s.substr(i, 10));
        }
        hash[h]++;
    }
    return ans;
}
```

</details>