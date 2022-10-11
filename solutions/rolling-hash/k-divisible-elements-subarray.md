## K Divisible Elements Subarray

```cpp
class Solution {
public:
    int countDistinct(vector<int>& nums, int k, int p) { 
        
        int P = 211, N = nums.size();
        unordered_set<unsigned long long>S;
        
        for (int i = 0; i < N; i++) {
            unsigned long long h = 0;
            int countDivisible = 0;
            
            for (int j = i; j < N; j++) {
                h = h * P + nums[j];
                countDivisible += (nums[j] % p == 0);
                
                if (countDivisible <= k) {
                    S.insert(h);
                } else {
                    break;
                }
            }
        }
        
        return (int)(S.size());
    }
};
```