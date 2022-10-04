# Custom Comparator

## Sort Array By Parity

```cpp
vector<int> sortArrayByParity(vector<int>& nums) {
    sort(nums.begin(), nums.end(), [&](int a, int b) {
        return (a % 2) < (b % 2); 
    });
    
    return nums;
}
```

## Sort The People

```cpp
vector<string> sortPeople(vector<string>& names, vector<int>& heights) {    
    int N = names.size();
    vector<int> idx(N, 0);
    iota(idx.begin(), idx.end(), 0);
    
    sort(idx.begin(), idx.end(), [&](int i, int j) {
        return heights[i] > heights[j]; 
    });
    
    vector<string> ans;
    
    for (auto &a : idx) {
        ans.push_back(names[a]);
    }
    
    return ans;
}
```

## Bitwise XOR of All Pairings

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int xorAllNums(vector<int>& nums1, vector<int>& nums2) {
        
        int ans = 0;
        int M = nums1.size(), N = nums2.size();
        
        if (N & 1) {
            ans = accumulate(nums1.begin(), nums1.end(), 0, [](int x, int y) {
                return x ^ y;
            });
        }
        
        if (M & 1) {
            ans ^= accumulate(nums2.begin(), nums2.end(), 0, [](int x, int y) {
                return x ^ y;
            });
        }
        
        return ans;
    }
};
```

</details>