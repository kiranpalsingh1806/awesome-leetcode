# Sieve of Eratosthenes

## Count Primes

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int countPrimes(int n) {
        vector<bool> primes(n + 1, true);
        
        int cntPrimes = 0;
        
        for(int i = 2; i < n; i++) {
            if(!primes[i]) continue;
            
            cntPrimes++;
            
            for(int j = i; j < n; j += i) {
                primes[j] = false;
            }
        }
        
        return cntPrimes;
    }
};
```

</details>

## Four Divisors

<details>
<summary> View Code </summary>

```cpp
class Solution {
    
    int num = 100001;
    void sieve_div(vector<int> &v, unordered_map<int,int>& m){
        for (int i = 1; i < num; i++) {
            for (int j = i; j < num; j += i){
                v[j]++;
                m[j] += i;
            }
        }
    }
public:
    int sumFourDivisors(vector<int>& nums) {
        long ans=0;
        vector<int> v(num, 0);
        
        unordered_map<int,int> m;
        
        sieve_div(v, m);
        
        int n = nums.size();
        
        for (int i = 0; i < n; i++) {
            if (v[nums[i]] == 4){
                ans += m[nums[i]];
            }
        }
        
        return ans;
    }
};
```

</details>