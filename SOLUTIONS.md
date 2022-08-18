- [1. Longest Increasing Subsequence](#1-longest-increasing-subsequence)
- [2. Generate Parentheses](#2-generate-parentheses)

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

## 2. Generate Parentheses

```cpp
class Solution {
public:
    
    vector<string> ans;
    
    void backtracking(string &temp, int leftCnt, int rightCnt) {
        
        // We found a valid parentheses.
        if(leftCnt == 0 && rightCnt == 0) {
            ans.push_back(temp);
            return;
        }
        
        // Include left parentheses
        
        if(leftCnt) {
            temp += "(";
            backtracking(temp, leftCnt - 1, rightCnt);
            temp.pop_back();
        }
        
        // Include right parentheses
        
        if(rightCnt > leftCnt) {
            temp += ")";
            backtracking(temp, leftCnt, rightCnt - 1);
            temp.pop_back();
        }
        
    }
    
    vector<string> generateParenthesis(int n) {
        string temp = "";
        backtracking(temp, n, n);
        
        return ans;
    }
};
```