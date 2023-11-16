# Sets

## 1. Find All Numbers Disappeared in an Array
```cpp
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {

        int n = nums.size();
        
        // Erase Duplicates from given array
        sort(nums.begin(), nums.end());
        nums.erase(unique(nums.begin(), nums.end()), nums.end());

        // Generate another vector from [1 ... n]
        vector<int> v(n);
        iota(v.begin(), v.end(), 1);

        // Which elements of v are not included in nums
        vector<int> notIncluded;
        set_difference(v.begin(), v.end(), nums.begin(), nums.end(), back_inserter(notIncluded));

        return notIncluded;
    }
};
```