
- [1. Longest Increasing Subsequence](#1-longest-increasing-subsequence)
- [2. Generate Parentheses](#2-generate-parentheses)
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
- [33. Flatten Binary Tree To Linked List](#33-flatten-binary-tree-to-linked-list)
- [37. Gas Station](#37-gas-station)
- [38. Max Points On A Line](#38-max-points-on-a-line)

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