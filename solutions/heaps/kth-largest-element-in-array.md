## Kth Largest Element in Array

```cpp
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<>> pq;
        for(auto N : nums) {
            pq.push(N);
            if(pq.size() > k) {
                pq.pop();
            }
        }
        return pq.top();
    }
};
```