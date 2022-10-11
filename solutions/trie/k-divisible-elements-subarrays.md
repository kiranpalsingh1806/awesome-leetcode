## K Divisible Elements Subarray

```cpp
struct Trie {
    unordered_map<int, Trie*> ch;
    int cnt = 0;
    int insert(vector<int>& nums, int i, int k, int p) {
        if (i == nums.size() || k - (nums[i] % p == 0) < 0) {
            return 0;
        }
        if (ch[nums[i]] == nullptr) {
            ch[nums[i]] = new Trie();
        }
        return (++ch[nums[i]]->cnt == 1) + 
            ch[nums[i]]->insert(nums, i + 1, k - (nums[i] % p == 0), p);
    }
};
int countDistinct(vector<int>& nums, int k, int p) {
    int res = 0;
    Trie t;
    for (int i = 0; i < nums.size(); ++i) {
        res += t.insert(nums, i, k, p);
    }
    return res;
}
```