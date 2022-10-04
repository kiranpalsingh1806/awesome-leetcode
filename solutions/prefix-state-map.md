# Prefix State Map

## Contiguous Array

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int findMaxLength(vector<int>& A) {
        
        unordered_map<int, int> M;
        int N = A.size();
        int sum = 0, ans = 0;
        
        M[0] = -1;
        
        for(int i = 0; i < N; i++) {
            sum += A[i] == 1 ? 1 : -1;
            
            if(M.count(sum)) {
                ans = max(ans, i - M[sum]);
            } else {
                M[sum] = i;
            }
        }
        
        return ans;
    }
};
```

</details>

## Find the Longest Substring Containing Vowels in Even Counts

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int findTheLongestSubstring(string s) {
        int ans = 0;
        int N = s.length();
        int h = 0;
        
        unordered_map<int, int> m{{'a', 0}, {'e', 1}, {'i', 2}, {'o', 3}, {'u', 4}};
        unordered_map<int, int> index{{0, -1}};
        
        for(int i = 0; i < N; i++) {
            if(m.count(s[i])) {
                h ^= (1 << m[s[i]]);
            }
            
            if(index.count(h)) {
                ans = max(ans, i - index[h]);
            } else {
                index[h] = i;
            }
        }
        
        return ans;
    }
};
```

</details>

## Number of Wonderful Substrings

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    long long wonderfulSubstrings(string s) {
        int N = s.size(), mask = 0;
        long long ans = 0, m[1024] = {1};
        for (int i = 0; i < N; ++i) {
            mask ^= 1 << (s[i] - 'a');
            ans += m[mask];
            for (int j = 0; j < 10; ++j) {
                int next = mask ^ (1 << j);
                ans += m[next];
            }
            m[mask]++;
        }
        return ans;
    }
};
```

</details>

## Find Longest Awesome Substring

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int longestAwesome(string s) {
        map<int, int> M;
        M[0] = -1;
        
        int N = s.length(), ans = 0;
        
        for(int i = 0, mask = 0; i < N; i++) {
            mask ^= (1 << (s[i] - '0'));
            
            if(M.count(mask)) ans = max(ans, i - M[mask]);
            else M[mask] = i;
            
            for(int j = 0; j < 10; j++) {
                int prev = mask ^ (1 << j);
                if(M.count(prev)) ans = max(ans, i - M[prev]);
            }
        }
        
        return ans;
    }
};
```

</details>