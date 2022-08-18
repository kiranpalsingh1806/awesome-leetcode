- [1. Longest Increasing Subsequence](#1-longest-increasing-subsequence)

## 1. Longest Increasing Subsequence

```cpp
int lengthOfLIS(vector<int>& nums) {
    int N = nums.size();
    
    vector<int> dp;
    
    for(int i = 0; i < N; i++) {
        
        auto it = lower_bound(dp.begin(), dp.end(), nums[i]);
        
        if(it != dp.end()) {
            *it = nums[i];
        } else {
            dp.push_back(nums[i]);
        }
    }
    
    return dp.size();
}
```