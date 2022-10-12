## Sort Array By Increasing Frequency

```cpp
class Solution {
public:
    vector<int> frequencySort(vector<int>& nums) {
        
        unordered_map<int, int> cnt;
        
        for(int n : nums) cnt[n]++;
        
        auto cmp = [&](int a, int b) {
            if(cnt[a] == cnt[b]) {
                return a < b;
            }
            return cnt[a] > cnt[b];
        };
        priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);
        
        for(auto &[n, c] : cnt) {
            pq.push(n);
        }
        
        vector<int> ans;
        
        while(pq.size()) {
            int c = pq.top();
            pq.pop();
            
            while(cnt[c]--) {
              ans.push_back(c);  
            }      
        }
        
        return ans;
    }
};
```