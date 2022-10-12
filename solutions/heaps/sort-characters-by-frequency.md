## Sort Characters By Frequency

```cpp
class Solution {
public:
    string frequencySort(string s) {
        
        unordered_map<char, int> cnt;
        
        for(char c : s) {
            cnt[c]++;
        }
        
        auto cmp = [&](char a, char b) { return cnt[a] < cnt[b]; };
        priority_queue<char, vector<char>, decltype(cmp)> pq(cmp);
        
        for(auto &[c, n] : cnt) {
            pq.push(c);
        }
        
        string ans = "";
        
        while(pq.size()) {
            char c = pq.top();
            pq.pop();
            
            ans += string(cnt[c], c);
        }
        
        return ans;
    }
};
```