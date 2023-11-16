# Base Conversion

## Find Unique Binary String

- Conversion of String to Number via stoi()
- Use of bitset

```cpp
class Solution {
public:
    string findDifferentBinaryString(vector<string>& nums) {

        unordered_set<int> integers;
        for (string num : nums) {
            integers.insert(stoi(num, 0, 2));
        }

        int n = nums.size();
        for (int num = 0; num <= n; num++) {
            if (integers.find(num) == integers.end()) {
                string ans = bitset<16>(num).to_string();
                return ans.substr(16 - n);
            }
        }

        return "";
    }
};
```
