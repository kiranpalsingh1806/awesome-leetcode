- [Dynamic Programming](#dynamic-programming)
  - [Climbing Stairs](#climbing-stairs)
  - [Pascal's Triangle](#pascals-triangle)
  - [Best Time To Buy and Sell Stock](#best-time-to-buy-and-sell-stock)
  - [Jump Game](#jump-game)
  - [Unique Paths](#unique-paths)
  - [Decode Ways](#decode-ways)
  - [Maximum Product Subarray](#maximum-product-subarray)
  - [House Robber](#house-robber)
  - [Word Break](#word-break)
  - [Coin Change](#coin-change)

# Dynamic Programming

## Climbing Stairs

<details>
<summary> View Code </summary>

```cpp
int climbStairs(int n) {
        
    if(n == 1) return 1;
    
    vector<int> dp(n, 0);
    
    dp[0] = 1;
    dp[1] = 2;
    
    for(int i = 2; i < n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }
    
    return dp[n - 1];
}
```

</details>



## Pascal's Triangle

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<vector<int>> generate(int N) {
        vector<vector<int>> ans(N);
        
        for(int i = 0; i < N; i++) {
            ans[i] = vector<int>(i + 1, 1);
            
            for(int j = 1; j < i; j++) {
                ans[i][j] = ans[i - 1][j] + ans[i - 1][j - 1];
            }
        }
        
        return ans;
        
    }
};
```

</details>


## Best Time To Buy and Sell Stock

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int N = prices.size();
        
        int minStock = prices[0];
        int profit = 0;
        
        for(int i = 0; i < N; i++) {
            minStock = min(minStock, prices[i]);
            
            profit = max(profit, prices[i] - minStock);
        }
        
        return profit;
    }
};
```

</details>


## Jump Game

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        
        int N = nums.size();
        int maxEnd = 0;
        
        for(int i = 0; i < N && maxEnd >= i; i++) {
            maxEnd = max(maxEnd, i + nums[i]);
        }
        
        return maxEnd >= N - 1;
    }
};
```

</details>


## Unique Paths

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<int> dp(n + 1, 0);
        dp[n - 1] = 1;
        
        for(int i = m - 1; i >= 0; i--) {
            for(int j = n - 1; j >= 0; j--){
                dp[j] += dp[j + 1];
            }
        }
        
        return dp[0];
    }
};
```

</details>


## Decode Ways

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int numDecodings(const string& s) {
        int N = s.size();
        vector<int> dp(N + 1, 0);
        dp[N] = 1;

        for (int i = N - 1; i >= 0; --i) {
            if (s[i] != '0') {
              dp[i] += dp[i + 1];
            }

            if (i+1 < N && (s[i] == '1' || s[i] == '2' && s[i + 1] <= '6')) {
              dp[i] += dp[i + 2];
            }
        }
        return dp[0];
    }
};
```

</details>


## Maximum Product Subarray

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int maxProduct(vector<int>& nums) {
        
        int maxProd = 1, minProd = 1;
        int ans = INT_MIN;
        
        for (int n : nums) {
            int a = maxProd * n;
            int b = minProd * n;
            
            maxProd = max({n, a, b});
            minProd = min({n, a, b});
            
            ans = max(ans, maxProd);
        }
        
        return ans;
    }
};
```

</details>


## House Robber

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        
        int N = nums.size();
        int rob = nums[0], notRob = 0;
        
        for (int i = 1; i < N; i++) {
            int temp = notRob;
            notRob = rob;
            rob = max(rob, temp + nums[i]);
        }
        
        return max(rob, notRob);
    }
};
```

</details>


## Word Break

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        
        unordered_set<string> M(wordDict.begin(), wordDict.end());
        
        int N = s.length();
        vector<bool> dp(N + 1, false);
        dp[0] = true;
        
        for (int i = 1; i <= N; i++) {
            for (int j = 0; j < i && !dp[i]; j++) {
                dp[i] = dp[j] && M.count(s.substr(j, i - j));
            }
        }
        
        return dp[N];
    }
};
```

</details>


## Coin Change

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        
        int N = coins.size();
        sort(coins.begin(), coins.end());
        vector<int> dp(amount + 1, INT_MAX);
        dp[0] = 0;
        
        for (int j = 1; j <= amount; j++) {
            
            dp[j] = INT_MAX;
            
            for (auto coin : coins) {
                if (j - coin < 0) break;
                
                if (dp[j - coin] != INT_MAX) {
                    dp[j] = min(dp[j], 1 + dp[j - coin]);
                }
            }
        }
        
        return dp[amount] == INT_MAX ? -1 : dp[amount];
    }
};
```

</details>