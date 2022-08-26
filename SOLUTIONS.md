
- [1. Longest Increasing Subsequence](#1-longest-increasing-subsequence)
- [2. Generate Parentheses](#2-generate-parentheses)
- [3. Sort Array By Parity](#3-sort-array-by-parity)
- [4. Min Cost To Connect All Points](#4-min-cost-to-connect-all-points)
- [5. Power(x, n)](#5-powerx-n)
- [6. Critical Connections In A Network](#6-critical-connections-in-a-network)
- [7. Longest Increasing Path In A Matrix](#7-longest-increasing-path-in-a-matrix)
- [8. Valid Arrangement of Pairs](#8-valid-arrangement-of-pairs)
- [9. Next Greater Element II](#9-next-greater-element-ii)
- [10. Container With Most Water](#10-container-with-most-water)
- [11. Implement Trie (Prefix Tree)](#11-implement-trie-prefix-tree)
- [12. Sort The Matrix Diagonally](#12-sort-the-matrix-diagonally)
- [13. Minimum Window Substring](#13-minimum-window-substring)
- [14. Increasing Triplet Subsequence](#14-increasing-triplet-subsequence)
- [15. Target Sum](#15-target-sum)
- [16. Check If There Is A Valid Partition For The Array](#16-check-if-there-is-a-valid-partition-for-the-array)
- [17. Longest Consecutive Sequence](#17-longest-consecutive-sequence)
- [18. Valid Sudoku](#18-valid-sudoku)
- [19. My Calendar I](#19-my-calendar-i)
- [20. Sliding Window Maximum](#20-sliding-window-maximum)
- [21. Best Time To Buy and Sell Stock](#21-best-time-to-buy-and-sell-stock)
- [22. Maximum Subarray](#22-maximum-subarray)
- [23. Cracking The Safe](#23-cracking-the-safe)
- [24. Find If Path Exists In Graph](#24-find-if-path-exists-in-graph)
- [25. Next Greater Node In Linked List](#25-next-greater-node-in-linked-list)
- [26. Repeated Substring Pattern](#26-repeated-substring-pattern)
- [27. Search Suggestion System](#27-search-suggestion-system)
- [28. Merge K Sorted Lists](#28-merge-k-sorted-lists)
- [29. Daily Temperatures](#29-daily-temperatures)
- [30. Merge Intervals](#30-merge-intervals)
- [31. Word Ladder](#31-word-ladder)
- [32. 3Sum](#32-3sum)
- [33. Flatten Binary Tree To Linked List](#33-flatten-binary-tree-to-linked-list)
- [34. Sum of Subarray Minimums](#34-sum-of-subarray-minimums)
- [35. Median of Two Sorted Arrays](#35-median-of-two-sorted-arrays)
- [36. LRU Cache](#36-lru-cache)
- [37. Gas Station](#37-gas-station)
- [38. Max Points On A Line](#38-max-points-on-a-line)
- [39. Largest Rectangle In Histogram](#39-largest-rectangle-in-histogram)
- [40. Regular Expression Matching](#40-regular-expression-matching)
- [41. Minimum Deletions To Make Character Frequencies Unique](#41-minimum-deletions-to-make-character-frequencies-unique)
- [42. Jump Game II](#42-jump-game-ii)
- [43. Count Good Nodes In Binary Tree](#43-count-good-nodes-in-binary-tree)
- [44. Unique Paths](#44-unique-paths)
- [45. Coin Change](#45-coin-change)
- [46. Is Graph Bipartite ?](#46-is-graph-bipartite-)
- [47. Frequency of Most Frequent Elements](#47-frequency-of-most-frequent-elements)
- [48. Group Anagrams](#48-group-anagrams)
- [49. Satisfiability of Equality Equations](#49-satisfiability-of-equality-equations)
- [50. Range Sum BST](#50-range-sum-bst)
- [51. Number of Islands](#51-number-of-islands)
- [52. Wildcard Matching](#52-wildcard-matching)
- [53. Min Stack](#53-min-stack)
- [54. Permutations](#54-permutations)
- [55. Combinations](#55-combinations)
- [56. Diameter of Binary Tree](#56-diameter-of-binary-tree)
- [57. Peak Index In Mountain Array](#57-peak-index-in-mountain-array)
- [58. Maximum Depth of Binary Tree](#58-maximum-depth-of-binary-tree)
- [59. Find Minimum In Rotated Sorted Array](#59-find-minimum-in-rotated-sorted-array)
- [60. Binary Tree Zigzag Level Order Traversal](#60-binary-tree-zigzag-level-order-traversal)
- [61. Longest Substring Without Repeating Characters](#61-longest-substring-without-repeating-characters)
- [62. Combination Sum](#62-combination-sum)
- [63. N-Queens](#63-n-queens)
- [64. Subsets](#64-subsets)
- [65. Pascal's Triangl](#65-pascals-triangl)

## 1. Longest Increasing Subsequence

```cpp
int lengthOfLIS(vector<int>& nums) {
    int N = nums.size();
    
    vector<int> dp;
    
    for(int i = 0; i < N; i++) {
        
        auto it = lower_bound(dp.begin(), dp.end(), nums[i]);
        
        if(it != dp.end()) {
            *it = nums[i];
        } else {
            dp.push_back(nums[i]);
        }
    }
    
    return dp.size();
}
```

## 2. Generate Parentheses

```cpp
class Solution {
public:
    
    vector<string> ans;
    
    void backtracking(string &temp, int leftCnt, int rightCnt) {
        
        // We found a valid parentheses.
        if(leftCnt == 0 && rightCnt == 0) {
            ans.push_back(temp);
            return;
        }
        
        // Include left parentheses
        
        if(leftCnt) {
            temp += "(";
            backtracking(temp, leftCnt - 1, rightCnt);
            temp.pop_back();
        }
        
        // Include right parentheses
        
        if(rightCnt > leftCnt) {
            temp += ")";
            backtracking(temp, leftCnt, rightCnt - 1);
            temp.pop_back();
        }
        
    }
    
    vector<string> generateParenthesis(int n) {
        string temp = "";
        backtracking(temp, n, n);
        
        return ans;
    }
};
```

## 3. Sort Array By Parity
```cpp
vector<int> sortArrayByParity(vector<int>& A) {
    sort(A.begin(), A.end(), [](int a, int b) {
        return a % 2 < b % 2;
    });
    
    return A;
}
```

## 4. Min Cost To Connect All Points
```cpp
class UnionFind {
    private:
        vector<int> id, rank;
        int cnt;
    public:
        UnionFind(int cnt) : cnt(cnt) {
            id = vector<int>(cnt);
            rank = vector<int>(cnt, 0);
            for (int i = 0; i < cnt; ++i) id[i] = i;
        }
        int find(int p) {
            if (id[p] == p) return p;
            return id[p] = find(id[p]);
        }
        int getCount() { 
            return cnt; 
        }
        bool connected(int p, int q) { 
            return find(p) == find(q); 
        }
        void connect(int p, int q) {
            int i = find(p), j = find(q);
            if (i == j) return;
            if (rank[i] < rank[j]) {
                id[i] = j;  
            } else {
                id[j] = i;
                if (rank[i] == rank[j]) rank[j]++;
            }
            --cnt;
        }
};

class Solution {
public:
    int minCostConnectPoints(vector<vector<int>>& points) {
        
        int N = points.size();
        
        vector<array<int, 3>> E;
        
        for(int i = 0; i < N; i++) {
            for(int j = i + 1; j < N; j++) {
                E.push_back({abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1]), i, j});
            }
        }
        
        UnionFind uf(N);
        
        int ans = 0;
        
        // How to convert vector into heap.
        make_heap(E.begin(), E.end(), greater<array<int, 3>>());
        
        while(uf.getCount() > 1) {
            pop_heap(E.begin(), E.end(), greater<array<int, 3>>());
            auto [w, u, v] = E.back();
            
            E.pop_back();
            
            if(uf.connected(u, v)) continue;
            
            uf.connect(u, v);
            ans += w;
        }
        
        return ans;
        
    }
};
```

## 5. Power(x, n)
```cpp
double recursion(double x, long n) {
        
    if(n < 0) {
        return 1 / recursion(x, -n);
    }
    
    if(n == 0) {
        return 1;
    }
    
    if(n == 1) {
        return x;
    }
    
    if(n == 2) {
        return x * x;
    }
    
    return recursion( recursion (x, n / 2), 2) * (n % 2 ? x : 1);
}

double myPow(double x, int n) {
    return recursion(x, (long)n);
}
```

## 6. Critical Connections In A Network
```cpp
class Solution {
public:
    vector<vector<int>> criticalConnections(int n, vector<vector<int>>& connections) {
        vector<int> ranks(n, INT_MIN);
        
        vector<vector<int>> G(n), ans;
        
        for(auto &e : connections) {
            int u = e[0], v = e[1];
            G[u].push_back(v);
            G[v].push_back(u);
        }
        
        function<int(int, int)> dfs = [&](int u, int rank) {
            if(ranks[u] >= 0) return ranks[u];
            
            ranks[u] = rank;
            int minRank = rank;
            
            for(int v : G[u]) {
                
                if(ranks[v] >= rank - 1) continue; 
                
                int neighbourMinRank = dfs(v, rank + 1);
                minRank = min(minRank, neighbourMinRank);
                
                if (neighbourMinRank > rank) {
                    ans.push_back({u, v});
                }
            }
            
            return minRank;
        };
        
        
        dfs(0, 0);
        return ans;
    }
};
```

## 7. Longest Increasing Path In A Matrix
```cpp
class Solution {
public:
    int M, N;
    vector<vector<int>> cnt;
    
    int dirs[4][2] = { {1, 0}, {0, 1}, {-1, 0}, {0, -1}};
    
    int dfs(vector<vector<int>> &A, int i, int j) {
        
        if(cnt[i][j] != -1e9) {
            return cnt[i][j];
        }
        
        cnt[i][j] = 1;
        
        for(auto &dir : dirs) {
            int a = i + dir[0];
            int b = j + dir[1];
            
            if(a < 0 || b < 0 || a >= M || b >= N || A[a][b] <= A[i][j]) continue;
            
            cnt[i][j] = max(cnt[i][j] , 1 + dfs(A, a, b));
        }
        
        return cnt[i][j];
    }
    
    int longestIncreasingPath(vector<vector<int>>& matrix) {
        M = matrix.size();
        N = matrix[0].size();
        
        cnt.assign(M, vector<int>(N, -1e9));
        
        int ans = 0;
        
        for(int i = 0; i < M; i++) {
            for(int j = 0; j < N; j++) {
                ans = max(ans, dfs(matrix, i, j));
            }
        }
        
        return ans;
    }
};
```

## 8. Valid Arrangement of Pairs
```cpp
class Solution {
public:
    vector<vector<int>> validArrangement(vector<vector<int>>& pairs) {
        unordered_map<int, vector<int>> G;
        unordered_map<int, int> indegrees, outdegrees;
        
        for(auto &e : pairs) {
            int u = e[0], v = e[1];
            G[u].push_back(v);
            indegrees[v]++;
            outdegrees[u]++;
        }
        
        // Select the starting node.
        int start = -1;
        
        for(auto &[u, ad] : G ) {
            if(outdegrees[u] - indegrees[u] == 1) {
                start = u;
                break;
            }
        }
        
        if(start == -1) {
            start = pairs[0][0];
        }
        
        vector<vector<int>> ans;
        
        function<void(int)> euler = [&](int u) {
            
            auto &ad = G[u];
            
            while(ad.size()) {
                int v = ad.back();
                ad.pop_back();
                
                euler(v);
                ans.push_back({u, v});
            }
        };
        
        euler(start);
        reverse(ans.begin(), ans.end());
        
        return ans;
    }
};
```

## 9. Next Greater Element II
```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int N = nums.size();
        
        // Stores index.
        stack<int> S;
        
        // Stores element
        vector<int> ans(N, -1);
        
        for(int i = 0; i < 2 * N; i++) {
            
            int n = nums[i % N];
            
            while(S.size() && nums[S.top()] < n) {
                ans[S.top()] = n;
                S.pop();
            }
            
            S.push(i % N);
        }
        
        return ans;
    }
};
```

## 10. Container With Most Water
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        
        int N = height.size();
        int L = 0, R = N - 1;
        
        int ans = 0;
        
        while(L < R) {
            int area = min(height[L], height[R]) * (R - L);
            
            ans = max(ans, area);
            
            if(height[L] < height[R]) {
                L++;
            } else {
                R--;
            }
        }
        
        return ans;
    }
};
```

## 11. Implement Trie (Prefix Tree)
```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    bool word = false;
};

class Trie {
    
    TrieNode root;
    
    TrieNode *find(string s) {
        
        auto node = &root;
        
        for(char c : s) {
            if(!node->next[c - 'a']) return NULL;
            
            node = node->next[c - 'a'];
        }
        
        return node;
    }
    
public:
    
    void insert(string word) {
        
        auto node = &root;
        
        for(char c : word) {
            if(!node->next[c - 'a']) node->next[c - 'a'] = new TrieNode();
            
            node = node->next[c - 'a'];
        }
        
        node->word = true;
    }
    
    bool search(string word) {
        auto wordFind = find(word);
        return wordFind && (wordFind->word == true);
    }
    
    bool startsWith(string prefix) {
        return find(prefix);
    }
};
```

## 12. Sort The Matrix Diagonally
```cpp
class Solution {
public:
    vector<vector<int>> diagonalSort(vector<vector<int>>& mat) {
        int M = mat.size();
        int N = mat[0].size();
        
        for (int i = 0; i < M; ++i) {
            vector<int> v;
            for (int x = i, y = 0; x < M && y < N; ++x, ++y) {
                v.push_back(mat[x][y]);
            }
            sort(v.begin(), v.end());
            int index = 0;
            for (int x = i, y = 0; x < M && y < N; ++x, ++y) {
                mat[x][y] = v[index++];
            }
        }
        
         for (int j = 1; j < N; ++j) {
             vector<int> v;
             for(int x = 0, y = j; x < M && y < N; ++x, ++y) {
                 v.push_back(mat[x][y]);
             }
             sort(v.begin(), v.end());
             int index = 0;
             for (int x = 0, y = j; x < M && y < N; ++x, ++y) {
                 mat[x][y] = v[index++];
             }
         }
        
        return mat;
    }
};
```

## 13. Minimum Window Substring
```cpp
class Solution {
public:
    string minWindow(string s, string t) {
        
        unordered_map<char, int> target, cnt;
        int N = s.length();
        
        // Store the frequency of target string
        for(char c : t) {
            target[c]++;
        }
        
        int matched = 0;
        int start = 0, len = INT_MAX;
        int i = 0;
        
        // Traverse the s string, j - right boundary, left boundary - 0
        for(int j = 0; j < N; j++) {
            
            if(++cnt[s[j]] <= target[s[j]]) matched++;
            
            // Target string comes inside this window substring.
            while(matched == t.size()) {
                
                // Update the answer start and its length
                if(len > j - i + 1) {
                    len = j - i + 1;
                    start = i;
                }
                
                // Decrease the length of window.
                if(--cnt[s[i]] < target[s[i]]) matched--;
                i++;
            }
            
        }
        
        if(len == INT_MAX) {
            return "";
        } else {
            return s.substr(start, len);
        }
    }
};
```

## 14. Increasing Triplet Subsequence
```cpp
class Solution {
public:
    bool increasingTriplet(vector<int>& nums) {
        
        int N = nums.size();
        
        vector<int> dp;
        
        for(int i = 0; i < N; i++) {
            
            auto it = lower_bound(dp.begin(), dp.end(), nums[i]);
            
            if(it != dp.end()) {
                *it = nums[i];
            } else {
                dp.push_back(nums[i]);
            }
        }
        
        return (dp.size() >= 3);
        
    }
};
```

## 15. Target Sum
```cpp
class Solution {
public:
    
    int recur(vector<int>& nums, int sum, int target, int i) {
        int n = nums.size();
        
        if(n == i) {
            // Check the sum if it is equal to target
            if(sum == target) return 1;
            
            return 0;
        }
        
        int res = 0;
        
        // Include
        res += recur(nums, sum + nums[i], target, i + 1);
        
        // Not Include
        res += recur(nums, sum - nums[i], target, i + 1);
        
        return res;
        
    }
    
    int findTargetSumWays(vector<int>& nums, int target) {
        // (vector, sum, target, index);
        return recur(nums, 0, target, 0);
    }
};

class Solution {
public:
    
    int recursion(vector<int>& nums, int i, int target, int n, vector<vector<int>> &dp) {
        if(i == n) {
            if(target == 0) return 1;
            return 0;
        }
        
        if(dp[i][target + 1000] != -1) return dp[i][target + 1000];
        
        int include = recursion(nums, i + 1, target + nums[i], n, dp);
        int notInclude = recursion(nums, i + 1, target - nums[i], n, dp);
        
        dp[i][target + 1000] = include + notInclude;
        return dp[i][target + 1000];
    }
    
    int findTargetSumWays(vector<int>& nums, int target) {
        
        vector<vector<int>> dp(nums.size() + 1, vector<int>(3000, -1));
        
        return recursion(nums, 0, target, nums.size(), dp);
    }
};
```

## 16. Check If There Is A Valid Partition For The Array
```cpp
class Solution {
public:
    bool validPartition(vector<int>& nums) {
        int N = nums.size();
        bool dp[N + 1];
        
        for(int i = 0; i <= N; i++) dp[i] = false;
        
        dp[0] = true;
        
        for(int i = 0; i < N; i++) {
            // for two elements
            if(i >= 1) {
                if(dp[i - 1] && nums[i] == nums[i - 1]) {
                    dp[i + 1] = true;
                }
            }
            
            // for three elements
            if(i >= 2) {
                if(dp[i - 2] && nums[i] == nums[i - 1] && nums[i - 1] == nums[i - 2]) {
                    dp[i + 1] = true;
                }
            }
            
            // for three consecutive elements
            if(i >= 2) {
                if(dp[i - 2] && nums[i] == nums[i - 1] + 1 && nums[i - 1] == nums[i - 2] + 1) {
                    dp[i + 1] = true;
                }
            }
        }
        
        return dp[N];
    }
};
```

## 17. Longest Consecutive Sequence
```cpp
// Union Find that also return the vector of size of components.
class UnionFind {
    vector<int> id, size;
public:
    UnionFind(int n) : id(n), size(n, 1) {
        for (int i = 0; i < n; ++i) id[i] = i;
    }
    void connect(int a, int b) {
        int x = find(a), y = find(b);
        if (x == y) return;
        id[x] = y;
        size[y] += size[x];
    }
    int find(int a) {
        return id[a] == a ? a : (id[a] = find(id[a]));
    }
    vector<int> &getSizes() {
        return size;
    }
};

class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        
        int N = nums.size();
        
        if(N == 0) {
            return 0;
        }
        
        UnionFind uf(N);
        
        unordered_map<int, int> M;
        
        // We have to store indexes in UnionFind instead of integer values.
        
        for(int i = 0; i < N; i++) {
            int n = nums[i];
            
            if(M.count(n)) continue;
            
            M[n] = i;
            
            if(M.count(n - 1)) uf.connect(M[n], M[n - 1]);
            if(M.count(n + 1)) uf.connect(M[n], M[n + 1]);
        }
        
        // ans -> maximum component size
        vector<int> ans = uf.getSizes();
        return *max_element(ans.begin(), ans.end());
    }
};
```

## 18. Valid Sudoku
```cpp
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int row[9][9] = {}, col[9][9] = {}, box[9][9] = {};
        
        for(int i = 0; i < 9; i++) {
            for(int j = 0; j < 9; j++) {
                int n = board[i][j] - '1';
                
                if(board[i][j] == '.') continue;
                
                if(row[i][n] || col[j][n] || box[(i / 3) * 3 + (j / 3)][n]) return false;
                
                
                row[i][n] = col[j][n] = box[i / 3 * 3 + j / 3][n] = 1;
            }
        }
        
        return true;
    }
};
```

## 19. My Calendar I
```cpp
class MyCalendar {
public:
    MyCalendar() {
        
    }

    map<int, int> M;
    
    bool book(int start, int end) {
        
        if(M.empty()) {
            M[start] = end;
            return true;
        }
        
        // Conditions 
        
        auto it = M.upper_bound(start);
        
        // Check the later intersection
        if(it != M.end() && it->first < end) return false;
        
        // Check the starting intersection
        if(it != M.begin() && prev(it)->second > start) return false;
        
        
        // After checking conditions
        M[start] = end;
        return true;
    }
};
```

## 20. Sliding Window Maximum
```cpp
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        int N = nums.size();
        deque<int> d; // Deque will store the index
        
        vector<int> ans;
        
        for(int i = 0; i < N; i++) {
            
            int n = nums[i];
            
            // When the element goes out of window, remove from the deque.
            if(d.size() && d.front() == i - k) d.pop_front();
            
            // We have to store monotonically decreasing sequence.
            while(d.size() && nums[d.back()]  <= n) {
                d.pop_back();
            }
            
            d.push_back(i);
            
            if(i >= k - 1) {
                // Push maximum element in answer.
                ans.push_back(nums[d.front()]);
            }
            
        }
        
        return ans;
    }
};
```

## 21. Best Time To Buy and Sell Stock
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

## 22. Maximum Subarray
```cpp
int maxSubArray(vector<int>& nums) {
    int global = nums[0];
    int local = 0;
    
    int N = nums.size();
    
    for(int i = 0; i < N; i++) {
        local = max(local + nums[i], nums[i]);
        global = max(global, local);
    }
    
    return global;
}
```

## 23. Cracking The Safe
```cpp
class Solution {
public:
    
    
    string crackSafe(int n, int k) {
        
        if(n == 1 && k == 1) return "0";
        
        // Store the edges of graph.
        unordered_set<string> M; 
        
        string start = string(n - 1, '0');
        string ans = "";
        
        function<void(string)> euler = [&](string u) {      
            for(char c = '0'; c < k + '0'; c++) {
                // How to use the last sequence optimally
                string v = u + c;

                // We don't have to visit the same edge again
                if(M.count(v)) continue;
                M.insert(v);
                
                euler(v.substr(1));

                ans.push_back(c);
            }
        };
        
        euler(start);
        
        return ans + start;
    }
};
```

## 24. Find If Path Exists In Graph
```cpp
class Solution {
public:
    bool validPath(int n, vector<vector<int>>& edges, int source, int destination) {
        
        // Creation of Graph
        unordered_map<int, vector<int>> G;
        
        for(auto &e : edges) {
            int u = e[0], v = e[1];
            G[u].push_back(v);
            G[v].push_back(u);
        }
        
        // BFS
        
        queue<int> q;
        vector<int> seen(n, 0); // 0 ->unseen
        
        q.push(source);
        seen[source] = 1;
        
        while(q.size()) {
            int v = q.front();
            q.pop();
            // Traverse every edge of v in breadth first search
            
            for(int u : G[v]) {
                if(seen[u]) continue;
                seen[u] = 1;
                q.push(u);
            }
        }
        
        if(seen[destination] == 1) {
            return true;
        } else {
            return false;
        }
    }
};
```

## 25. Next Greater Node In Linked List
```cpp
class Solution {
public:
    
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = new ListNode();
        
        while(head) {
            auto node = head;
            head = head->next;
            node->next = prev->next;
            prev->next = node;
        }

        return prev->next;
    }
    
    vector<int> nextLargerNodes(ListNode* head) {
        head = reverseList(head);
        
        stack<int> S;
        vector<int> ans;
        
        
        while(head) {
            
            int n = head->val;
            
            while(S.size() && S.top() <= n) {
                S.pop();
            }
            
            if(S.size() == 0) {
                ans.push_back(0);
            } else {
                ans.push_back(S.top());
            }
            
            S.push(n);
            
            head = head->next;
        }
        
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

## 26. Repeated Substring Pattern
```cpp
class Solution {
public:
    bool repeatedSubstringPattern(string s) {
        int N = s.length();
        
        for(int len = 1; len <= N / 2; len++) {
            if(N % len) continue;
            
            int i = len;
            for(; i < N; i++) {
                if( s[i] != s[i % len]) break;
            }
            
            if(i == N) return true;
        }
        
        return false;
    }
};
```

## 27. Search Suggestion System
```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    int index = -1;
};

void add(TrieNode *node, string &s, int i) {
    
    for(char c: s) {
        if(!node->next[c - 'a']) node->next[c - 'a'] = new TrieNode();
        node = node->next[c - 'a'];
    }
    node->index = i;
}

void collect(TrieNode *node, vector<string> &ans, vector<string> &products) {
    if(ans.size() == 3) return;
    
    if(!node) return;
    
    if(node->index > -1) ans.push_back(products[node->index]);
    
    for(int i = 0; i < 26; i++) {
        if(node->next[i]) collect(node->next[i], ans, products);
    }
}

class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        TrieNode root, *node = &root;
        
        for(int i = 0; i < products.size(); i++) {
            add(&root, products[i], i);
        }
        
        vector<vector<string>> ans(searchWord.size());
        
        for(int i = 0; i < searchWord.length(); i++) {
            node = node->next[searchWord[i] - 'a'];
            
            if(!node) break;
            
            collect(node, ans[i], products);
        }
        
        return ans;
    }
};
```

## 28. Merge K Sorted Lists
```cpp
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        ListNode dummy, *tail = &dummy;
        auto cmp = [](auto a, auto b) { return a->val > b->val; };
        priority_queue<ListNode*, vector<ListNode*>, decltype(cmp)> q(cmp);
        for (auto list : lists) {
            if (list) q.push(list); // avoid pushing NULL list.
        }
        while (q.size()) {
            auto node = q.top();
            q.pop();
            if (node->next) q.push(node->next);
            tail->next = node;
            tail = node;
        }
        return dummy.next;
    }
};
```

## 29. Daily Temperatures
```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& A) {
        stack<int> s;
        vector<int> ans(A.size());
        for (int i = A.size() - 1; i >= 0; --i) {
            while (s.size() && A[s.top()] <= A[i]) s.pop();
            ans[i] = s.size() ? s.top() - i : 0;
            s.push(i);
        }
        return ans;
    }
};
```

## 30. Merge Intervals
```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        sort(intervals.begin(), intervals.end());
        vector<vector<int>> ans;
        
        for(auto &a : intervals) {
            if(!ans.size() || a[0] > ans.back()[1]) {
                ans.push_back(a);
            } else if(ans.back()[1] < a[1]) {
                ans.back()[1] = a[1];
            }
        }
        
        return ans;
    }
};
```

## 31. Word Ladder
```cpp
int ladderLength(string beginWord, string endWord, vector<string>& wordList) {
    unordered_set<string> s(begin(wordList), end(wordList));
    if (s.count(endWord) == 0) return 0;
    queue<string> q{{beginWord}};
    s.erase(beginWord);
    int step = 1;
    while (q.size()) {
        int cnt = q.size();
        while (cnt--) {
            auto u = q.front();
            q.pop();
            if (u == endWord) return step;
            for (char &c : u) { // add unvisited neighbors of `u`
                char tmp = c;
                for (char ch = 'a'; ch <= 'z'; ++ch) {
                    if (tmp == ch) continue;
                    c = ch;
                    if (s.count(u) == 0) continue;
                    s.erase(u);
                    q.push(u);
                }
                c = tmp;
            }
        }
        ++step;
    }
    return 0;
}
```

## 32. 3Sum
```cpp
vector<vector<int>> threeSum(vector<int>& A) {
    vector<vector<int>> ans;
    sort(A.begin(), A.end());
    
    int N = A.size();
    int L = 0, R = N - 1;
    
    for(int i = 0; i < N - 2; i++) {
        
        if(i > 0 && A[i] == A[i - 1]) continue;
        
        int L = i + 1, R = N - 1;
        
        while(L < R) {
            int sum = A[i] + A[L] + A[R];
            
            if(sum == 0) {
                ans.push_back({A[i], A[L], A[R]});
            }
            
            if(sum <= 0) {
                L++;

                while(L < R && A[L] == A[L - 1]) L++;
            }
            
            if(sum >= 0) {
                R--;

                while(L < R && A[R] == A[R + 1]) R--;
            }
        }
    }
    
    return ans;
}
```

## 33. Flatten Binary Tree To Linked List
```cpp
void flatten(TreeNode* root) {
    if(!root) return;
    TreeNode *tail = nullptr;
    
    stack<TreeNode*> S;
    
    S.push({root});
    
    while(S.size()) {
        auto node = S.top();
        S.pop();
        
        if(tail) tail->right = node;
        tail = node;
        
        if(node->right) S.push(node->right);
        if(node->left) S.push(node->left);
        
        node->left = node->right = nullptr;
    }
}
```

## 34. Sum of Subarray Minimums
```cpp
int sumSubarrayMins(vector<int>& A) {
    stack<int> q;
    q.push(-1);
    long N = A.size(), ans = 0, sum = 0, mod = 1e9+7;
    for (int i = 0; i < N; ++i) {
        sum = (sum + A[i]) % mod;
        while (q.top() != -1 && A[q.top()] >= A[i]) {
            int j = q.top();
            q.pop();
            int c = j - q.top();
            sum = (sum + c * (A[i] - A[j]) % mod) % mod;
        }
        q.push(i);
        ans = (ans + sum) % mod;
    }
    return ans;
}
```

## 35. Median of Two Sorted Arrays
```cpp
double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
    if (nums1.size() > nums2.size()) swap(nums1, nums2);
    int M = nums1.size(), N = nums2.size(), L = 0, R = M, K = (M + N + 1) / 2;
    while (true) {
        int i = (L + R) / 2, j = K - i;
        if (i < M && nums2[j - 1] > nums1[i]) L = i + 1;
        else if (i > L && nums1[i - 1] > nums2[j]) R = i - 1;
        else {
            int maxLeft = max(i ? nums1[i - 1] : INT_MIN, j ? nums2[j - 1] : INT_MIN);
            if ((M + N) % 2) return maxLeft;
            int minRight = min(i == M ? INT_MAX : nums1[i], j == N ? INT_MAX : nums2[j]);
            return (maxLeft + minRight) / 2.0;
        }
    }
}
```

## 36. LRU Cache
```cpp
class LRUCache {
    int capacity;
    list<pair<int, int>> data;
    unordered_map<int, list<pair<int, int>>::iterator> m;
    void moveToFront(int key) {
        auto node = m[key];
        data.splice(data.begin(), data, node);
        m[key] = data.begin();
    }
public:
    LRUCache(int capacity) : capacity(capacity) {}
    int get(int key) {
        // get node given key, put the node at the beginning of the list, return the value in the node
        if (m.count(key)) {
            moveToFront(key);
            return m[key]->second;
        }
        return -1;
    }
    void put(int key, int value) {
        // if key exists in the map, get node given key, put the node at the beginning of the list and update the value in the node
        // otherwise, put a new node at the beginning of the list with the <key, value> and update the map. If capacity exceeded, remove the last node from the list and map.
        if (m.count(key)) {
            moveToFront(key);
            m[key]->second = value;
        } else {
            data.emplace_front(key, value);
            m[key] = data.begin();
            if (data.size() > capacity) {
                m.erase(data.rbegin()->first);
                data.pop_back();
            }
        }
    }
};
```

## 37. Gas Station
```cpp
int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
    int N = gas.size(), len = 0, start = 0;
    for (int i = 0, sum = 0; i < 2 * N && len < N; ++i) {
        sum += gas[i % N] - cost[i % N];
        if (sum < 0) {
            len = sum = 0;
            start = (i + 1) % N;
        } else ++len;
    }
    return len == N ? start : -1;
}
```

## 38. Max Points On A Line
```cpp
class Solution {
public:
    int maxPoints(vector<vector<int>>& points) {
        
        int res = 0;
        for(int i = 0; i<points.size(); i++){
            
            unordered_map<long double,int> noOfPointsInLine;
            
            for(int j = i + 1; j < points.size(); j++){
                
                int x1 = points[i][0], y1 = points[i][1], x2 = points[j][0], y2 = points[j][1];
                
                if(y2 == y1) {     
                    noOfPointsInLine[INT_MIN]++;
                } else if(x1 == x2){ 
                    noOfPointsInLine[INT_MAX]++;
                } else {               
                    long double slope = (long double)(y2 - y1) /(long double)(x2 - x1);
                    noOfPointsInLine[slope]++;
                }
                
            }
            
            for(auto i : noOfPointsInLine){
                res = max(i.second, res);
            }
        }
        return res + 1;
    }
};
```

## 39. Largest Rectangle In Histogram
```cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& A) {
        int N = A.size();
        
        int ans = 0;
        
        stack<int> S;
        vector<int> next(N, N), prev(N, -1);
        
        for(int i = 0; i < N; i++) {
            while(S.size() && A[i] < A[S.top()]) {
                next[S.top()] = i;
                S.pop();
            }
            S.push(i);
        }
        
        for(int i = N - 1; i >= 0; i--) {
            while(S.size() && A[i] < A[S.top()]) {
                prev[S.top()] = i;
                S.pop();
            }
            S.push(i);
        }
        
        for(int i = 0; i < N; i++) {
            ans = max(ans, A[i] * (next[i] - prev[i] - 1));
        }
        
        return ans;
    }
};
```

## 40. Regular Expression Matching
```cpp
class Solution {
private:
    inline bool matchChar(string &s, int i, string &p, int j) {
        return p[j] == '.' ? i < s.size() : s[i] == p[j];
    }
    bool isMatch(string s, int i, string p, int j) {
        if (j == p.size()) return i == s.size();
        if (j + 1 < p.size() && p[j + 1] == '*') {
            bool ans = false;
            while (!(ans = isMatch(s, i, p, j + 2))
            && matchChar(s, i, p, j)) ++i;
            return ans;
        } else {
            return matchChar(s, i, p, j) && isMatch(s, i + 1, p, j + 1);
        }
    }
public:
    bool isMatch(string s, string p) {
        return isMatch(s, 0, p, 0);
    }
};
```

## 41. Minimum Deletions To Make Character Frequencies Unique
```cpp
class Solution {
public:
    int minDeletions(string s) {
        int cnt[26] = {0};
        set<int> S;
        int ans = 0;
        for (char c : s) {
          cnt[c - 'a']++;  
        } 
        
        for(int i = 0; i < 26; i++) {
            while(cnt[i]-- && !S.insert(cnt[i]).second) {
                ans++;
            }
        }
        return ans;
    }
};
```

## 42. Jump Game II
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int N = nums.size();
        vector<int> dp(N, 1e9);
        
        dp[0] = 0;
        
        for(int i = 0; i < N; i++) {
            for(int j = 1; j <= nums[i] && i + j < N; j++) {
                dp[i + j] = min(dp[i + j], 1 + dp[i]);
            }
        }
        
        return dp[N - 1];
    }
};
```

## 43. Count Good Nodes In Binary Tree
```cpp
class Solution {
public:
    int ans = 0;
    int dfs(TreeNode* root, int maxVal) {
        if(root->val >= maxVal) {
            ans++;
        }
        maxVal = max(maxVal, root->val);
        
        if(root->left) {
            dfs(root->left, maxVal);
        }
        
        if(root->right) {
            dfs(root->right, maxVal);
        }
        
        return ans;
    }
    int goodNodes(TreeNode* root) {
        return dfs(root, INT_MIN);
    }
};
```

## 44. Unique Paths
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

## 45. Coin Change
```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int dp[amount + 1];
        dp[0] = 0;
        
        sort(coins.begin(), coins.end());
        
        for(int i = 1; i <= amount; i++) {
            
            dp[i] = INT_MAX;
            for(auto &coin : coins) {
                if(i - coin < 0) break;
                
                if(dp[i - coin] != INT_MAX) {
                    dp[i] = min(dp[i], 1 + dp[i - coin]);
                }
            }
        }
        
        if(dp[amount] != INT_MAX) {
            return dp[amount];
        } else {
            return -1;
        }
    }
};
```

## 46. Is Graph Bipartite ?
```cpp
class Solution {
public:
    bool isBipartite(vector<vector<int>>& G) {
        int N = G.size();
        vector<int> id(N); // 0 unseen, 1 and -1 are different colors
        function<bool(int, int)> dfs = [&](int u, int color) {
            if (id[u]) return id[u] == color;
            id[u] = color;
            for (int v : G[u]) {
                if (!dfs(v, -color)) return false;
            }
            return true;
        };
        for (int i = 0; i < N; ++i) {
            if (!id[i] && !dfs(i, 1)) return false;
        }
        return true;
    }
};
```

## 47. Frequency of Most Frequent Elements
```cpp
class Solution {
public:
    int maxFrequency(vector<int>& A, int k) {
        int N = A.size();
        
        sort(A.begin(), A.end());
        
        long ans = 1, sum = 0, i = 0;
        
        for(int j = 0; j < N; j++) {
            sum += A[j];
            
            // Increase the left boundary of window :
            // (Length of window * currentElement) - Sum of all elements > k 
            while( (j - i + 1) * A[j] - sum > k) {
                sum -= A[i++];
            }
            
            ans = max(ans, j - i + 1);
            
        }
        
        return ans;
    }
};
```

## 48. Group Anagrams
```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        
        unordered_map<string, vector<string>> M;
        
        for(string &s : strs) {
            
            string t = s;
            sort(t.begin(), t.end());
            
            M[t].push_back(s);
        }
        
        vector<vector<string>> ans;
        
        for(auto &[s, vs] : M) {
            ans.push_back(vs);    
        }
        
        return ans;
    }
};
```

## 49. Satisfiability of Equality Equations
```cpp
class UnionFind {
    private:
        vector<int> id, rank;
        int cnt;
    public:
        UnionFind(int cnt) : cnt(cnt) {
            id = vector<int>(cnt);
            rank = vector<int>(cnt, 0);
            for (int i = 0; i < cnt; ++i) id[i] = i;
        }
        int find(int p) {
            if (id[p] == p) return p;
            return id[p] = find(id[p]);
        }
        int getCount() { 
            return cnt; 
        }
        bool connected(int p, int q) { 
            return find(p) == find(q); 
        }
        void connect(int p, int q) {
            int i = find(p), j = find(q);
            if (i == j) return;
            if (rank[i] < rank[j]) {
                id[i] = j;  
            } else {
                id[j] = i;
                if (rank[i] == rank[j]) rank[j]++;
            }
            --cnt;
        }
};

class Solution {
public:
    bool equationsPossible(vector<string>& equations) {
        int N = equations.size();
        
        UnionFind uf(26);
        
        for(auto &e : equations) {
            if(e[1] == '=') {
                int num1 = e[0] - 'a';
                int num2 = e[3] - 'a';
                uf.connect(num1, num2);
            }
        }
        
        for(auto &e : equations) {
            if(e[1] == '!') {
                int num1 = e[0] - 'a';
                int num2 = e[3] - 'a';
                if(uf.connected(num1, num2)) {
                    return false;
                }
            }
        }
        
        return true;
    }
};
```

## 50. Range Sum BST
```cpp
class Solution {
public:
    int sum = 0;
    
    void preorder(TreeNode* root, int L, int R) {
        if(!root) {
            return;
        }
        
        if(root->val >= L && root->val <= R) {
            sum += root->val;
        }
        
        preorder(root->left, L, R);
        preorder(root->right, L, R);
    }
    
    int rangeSumBST(TreeNode* root, int low, int high) {
        preorder(root, low, high);
        return sum;
    }
};
```

## 51. Number of Islands
```cpp
class Solution {
public:
    
    int M, N;
    
    int dirs[4][2] = { {0, 1}, {1, 0}, {-1, 0}, {0, -1}};
    
    void dfs(vector<vector<char>> &grid, int i, int j) {
        
        // This cell of grid has been visited.
        grid[i][j] = '2';
        
        // Go to the four sides of grid.
        for(auto &dir : dirs) {
            int a = i + dir[0];
            int b = j + dir[1];
            
            if(a < 0 || b < 0 || a >= M || b >= N || grid[a][b] != '1') continue;
            
            dfs(grid, a, b);
        }
    }
    
    int numIslands(vector<vector<char>>& grid) {
        M = grid.size();
        N = grid[0].size();
        
        int islandCnt = 0;
        
        for(int i = 0; i < M; i++) {
            for(int j = 0; j < N; j++) {
                if(grid[i][j] == '1') {
                    dfs(grid, i, j);
                    islandCnt++;
                }
            }
        }
        
        return islandCnt;
    }
};
```

## 52. Wildcard Matching
```cpp
class Solution {
public:
    
    int M, N;
    vector<vector<int>> dp;
    
    bool wildcardMatching(string &s, string &p, int i, int j) {
        
        if(dp[i][j] != -1) return dp[i][j]; 
        int &ans = dp[i][j];
        
        for(; j < N; j++) {
            
            if(p[j] != '*' && i >= M) return ans = false;
            if(p[j] == '?') {
                i++;
            } else if(p[j] == '*') {
                while(j + 1 < N && p[j + 1] == '*') j++;
                for(int k = 0; i + k <= M; i++) {
                    if(wildcardMatching(s, p, i + k, j + 1)) {
                        return ans = true;
                    }
                }
            } else if(s[i++] != p[j]) {
                return ans = false;
            }
        }
        
        return ans = i >= M;
        
    }
    
    bool isMatch(string s, string p) {
        M = s.size();
        N = p.size();
        
        dp.assign(M + 1, vector<int>(N + 1, -1));
        return wildcardMatching(s, p, 0, 0);
    }
};
```

## 53. Min Stack
```cpp
class MinStack {
public:
    
    stack<int> S, M;
    
    void push(int val) {
        S.push(val);
        if(M.empty() || M.top() >= val) {
            M.push(val);
        }
    }
    
    void pop() {
        int x = S.top();
        S.pop();
        
        // If popped element is minimum
        if(M.top() == x) {
            M.pop();
        }
    }
    
    int top() {
        return S.top();
    }
    
    int getMin() {
        return M.top();
    }
};
```

## 54. Permutations
```cpp
class Solution {
public:
    
    vector<vector<int>> ans;
    
    void permute(vector<int> &nums, int start) {
        // Base case
        if(start == nums.size()) {
            ans.push_back(nums);
            return;
        }
        
        for(int i = start; i < nums.size(); i++) {
            swap(nums[start], nums[i]);
            permute(nums, start + 1);
            swap(nums[start], nums[i]);
        }
        
    }
    
    vector<vector<int>> permute(vector<int>& nums) {
        permute(nums, 0);
        return ans;
    }
};
```

## 55. Combinations
```cpp
class Solution {
public:
    
    vector<vector<int>> ans;
    
    void combine(vector<int> &temp, int n, int k, int start) {
        // Base case
        if(temp.size() == k) {
            ans.push_back(temp);
            return;
        }
        
        for(int i = start, end = n - k + temp.size(); i <= end; i++) {
            temp.push_back(i + 1);
            combine(temp, n, k, i + 1);
            temp.pop_back();
        }
    }
    
    vector<vector<int>> combine(int n, int k) {
        vector<int> temp;
        combine(temp, n, k, 0);
        return ans;
    }
};
```

## 56. Diameter of Binary Tree
```cpp
class Solution {
public:
    int diameter = 0;

    int dfs(TreeNode* root) {
        if(!root) {
            return 0;
        }
        
        int left = dfs(root->left);
        int right = dfs(root->right);
        
        diameter = max(diameter, left + right);
        
        return (1 + max(left, right));
    }
    
    int diameterOfBinaryTree(TreeNode* root) {
        dfs(root);
        return diameter;
    }
};
```

## 57. Peak Index In Mountain Array
```cpp
int peakIndexInMountainArray(vector<int>& arr) {
    int N = arr.size();
    
    int L = 1, R = N - 2, M;
    
    while(L <= R) {
        M = (L + R) / 2;
        
        if(arr[M] > arr[M - 1]) {
            L = M + 1;
        } else {
            R = M - 1;
        }
    }
    
    return R;
}
```

## 58. Maximum Depth of Binary Tree
```cpp
int maxDepth(TreeNode* root) {
    if(!root) {
        return 0;
    }
    
    return (1 + max(maxDepth(root->left), maxDepth(root->right)));
}
```

## 59. Find Minimum In Rotated Sorted Array
```cpp
int findMin(vector<int>& nums) {
    int N = nums.size();
    
    int L = 0, R = N - 1, M;
    
    while(L < R) {
        M = (L + R) / 2;
        
        if(nums[M] < nums[R]) {
            R = M;
        } else {
            L = M + 1;
        }
    }
    
    return nums[R];
}
```

## 60. Binary Tree Zigzag Level Order Traversal
```cpp
class Solution {
public:
    
    vector<vector<int>> ans;
    
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        if(!root) {
            return {};
        }
        
        bool l2r = true;
        
        queue<TreeNode*> q;
        q.push({root});
        
        while(q.size()) {
            int cnt = q.size();
            
            vector<int> temp;
            
            while(cnt--) {
                auto node = q.front();
                q.pop();
                
                temp.push_back(node->val);
                
                if(node->left) {
                    q.push(node->left);
                }
                
                if(node->right) {
                    q.push(node->right);
                }
            }
            
            if(!l2r) {
                reverse(temp.begin(), temp.end());
            }
            
            l2r = !l2r;
            ans.push_back(temp);
        }
        
        return ans;
    }
};
```

## 61. Longest Substring Without Repeating Characters
```cpp
int lengthOfLongestSubstring(string s) {
    int N = s.length();
    int length = 0, i = 0;
    unordered_map<int, int> M;
    
    for(int j = 0; j < N; j++) {
        
        M[s[j]]++;
        
        // Increase the window size from left side if there are multiple characters
        while(M[s[j]] > 1) {
            M[s[i++]]--;
        }
        
        length = max(length, j - i + 1);
    }
    
    return length;
}
```

## 62. Combination Sum
```cpp
vector<vector<int>> combinationSum(vector<int>& A, int target) {
    vector<vector<int>> ans;
    vector<int> tmp;
    sort(begin(A), end(A));
    function<void(int, int)> dfs = [&](int start, int goal) {
        if (goal == 0) {
            ans.push_back(tmp);
        }
        for (int i = start; i < A.size() && gaol - A[i] >= 0; ++i) {
            tmp.push_back(A[i]);
            dfs(i, goal - A[i]);
            tmp.pop_back();
        }
    };
    dfs(0, target);
    return ans;
}
```

## 63. N-Queens
```cpp
class Solution {
    vector<vector<string>> ans;
    vector<string> B;
    vector<bool> col, hill, dale;
    int n;
    void dfs(int i) {
        if (i == n) {
            ans.push_back(B);
            return;
        }
        for (int j = 0; j < n; ++j) {
            int h = i + j, d = i + n - 1 - j;
            if (col[j] || hill[h] || dale[d]) continue;
            col[j] = hill[h] = dale[d] = true;
            B[i][j] = 'Q';
            dfs(i + 1);
            B[i][j] = '.';
            col[j] = hill[h] = dale[d] = false;
        }
    }
public:
    vector<vector<string>> solveNQueens(int n) {
        this->n = n;
        B.assign(n, string(n, '.'));
        col.assign(n, false);
        hill.assign(2 * n - 1, false);
        dale.assign(2 * n - 1, false);
        dfs(0);
        return ans;
    }
};
```

## 64. Subsets
```cpp
vector<vector<int>> subsets(vector<int>& A) {
    vector<vector<int>> ans;
    vector<int> tmp;
    function<void(int)> dfs = [&](int i) {
        if (i == A.size()) {
            ans.push_back(tmp);
            return;
        }
        tmp.push_back(A[i]);
        dfs(i + 1); // Pick A[i]
        tmp.pop_back();
        dfs(i + 1); // Skip A[i]
    };
    dfs(0);
    return ans;
}
```

## 65. Pascal's Triangl
```cpp
vector<vector<int>> generate(int numRows) {
    vector<vector<int>> ans(numRows);
    for (int i = 0; i < numRows; ++i) {
        ans[i] = vector<int>(i + 1, 1);
        for (int j = 1; j < i; ++j) ans[i][j] = ans[i - 1][j - 1] + ans[i - 1][j];
    }
    return ans;
}
```