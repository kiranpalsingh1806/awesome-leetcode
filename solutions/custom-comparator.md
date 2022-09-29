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
    
    sort(idx.begin(), idx.end(), [&](auto &i, auto &j) {
        return heights[i] > heights[j]; 
    });
    
    vector<string> ans;
    
    for (auto &a : idx) {
        ans.push_back(names[a]);
    }
    
    return ans;
}
```