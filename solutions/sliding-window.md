# Sliding Window

## Longest Substring Without Repeating Characters

```cpp
int lengthOfLongestSubstring(string s) {
    int N = s.length();
    int ans = 0, i = 0;
    
    unordered_map<char, int> M;
    
    for(int j = 0; j < N; j++) {
        
        M[s[j]]++;
        
        // Window size increases from left side.
        while(M[s[j]] > 1) {
            M[s[i++]]--;
        }
        
        ans = max(ans, j - i + 1);
    }
    
    return ans;
}
```

## Minimum Size Subarray Sum

```cpp
int minSubArrayLen(int target, vector<int>& nums) { 
    int N = nums.size();
    int sum = 0, ans = N + 1, i = 0;
    
    for(int j = 0; j < N; j++) {
        
        sum += nums[j];
        
        while(sum >= target) {
            ans = min(ans, j - i + 1);
            sum -= nums[i++];
        }
    }
    
    return ans == N + 1 ? 0 : ans;
}
```

## Number of Smooth Descent Periods of a Stock

```cpp
long long getDescentPeriods(vector<int>& prices) {   
    long long ans = 0;
    int i = 0, N = prices.size();
    
    for(int j = 0; j < N; j++) {
        
        if(j && prices[j] + 1 != prices[j - 1]) {
            i = j;
        }
        
        ans += (j - i + 1);
    }
    
    return ans;
}
```

## Frequency of Most Frequent Element

```cpp
int maxFrequency(vector<int>& A, int k) {
    sort(A.begin(), A.end());
    int N = A.size();
    
    long long i = 0, sum = 0, ans = 0;
    
    for(int j = 0; j < N; j++) {
        sum += A[j];
        
        // Increase the windows size when our total sum - sum of window > k
        while((A[j] * (j - i + 1) - sum) > k ) {
            sum -= A[i++];
        }
        
        // If our window is valid, we can perform less than or equal to k operations.
        ans = max(ans, j - i + 1);
    }
    
    return ans;
}
```

## Max Consecutive Ones III

```cpp
int longestOnes(vector<int>& nums, int k) {  
    int N = nums.size();
    int length = 0, i = 0, sum = 0;
    
    for(int j = 0; j < N; j++) {
        sum += nums[j];
        while(((j - i + 1) - sum) > k) {
            sum -= nums[i++];
        }
        
        length = max(length, j - i + 1);
    }
    
    return length;
}
```