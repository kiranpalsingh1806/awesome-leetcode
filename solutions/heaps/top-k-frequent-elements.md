## Top K Frequent Elements

```cpp
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        
        unordered_map<int, int> cnt;
        
        auto cmp = [&](int a, int b) { return cnt[a] > cnt[b]; };
        priority_queue<int, vector<int>, decltype(cmp)> pq(cmp);
        
        for(int n : nums) cnt[n]++;
        
        for(auto &[n, c] : cnt) {
            pq.push(n);
        }
        
        vector<int> ans;
        
        while(pq.size() > k) {
            int c = pq.top();
            pq.pop();
        } 
        
        while(pq.size()) {
            int c = pq.top();
            pq.pop();
            ans.push_back(c);
        }
        
        return ans;
    }
};
```