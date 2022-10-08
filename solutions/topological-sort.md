# Topological Sort

## Course Schedule

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    bool canFinish(int k, vector<vector<int>>& prerequisites) {
        
        // Creation of Graph
        unordered_map<int, vector<int>> G;
        vector<int> indegree(k, 0);
        for (auto &e : prerequisites) {
            int u = e[0], v = e[1];
            G[v].push_back(u);
            indegree[u]++;
        }
        
        // Queue to store the nodes with zero indegree - Topological Sort  
        queue<int> q;
        
        for (int i = 0; i < k; i++) {
            if (indegree[i] == 0) {
                q.push(i);
            }
        }
        
        while (q.size()) {
            int cnt = q.size();
            
            while(cnt--) {
                int u = q.front();
                q.pop();
                k--;
                for(auto v : G[u]) {
                    if(--indegree[v] == 0) {
                        q.push(v);
                    }
                }
            }
        }
        
        return k == 0;
    }
};
```

</details>

## Minimum Height Trees

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<int> findMinHeightTrees(int n, vector<vector<int>>& E) {
        if (n == 1) return { 0 };
        vector<int> degree(n), ans;
        vector<vector<int>> G(n);
        for (auto &e : E) {
            int u = e[0], v = e[1];
            degree[u]++;
            degree[v]++;
            G[u].push_back(v);
            G[v].push_back(u);
        }
        queue<int> q;
        for (int i = 0; i < n; ++i) {
            if (degree[i] == 1) q.push(i);
        }
        while (n > 2) {
            int cnt = q.size();
            n -= cnt;
            while (cnt--) {
                int u = q.front();
                q.pop();
                for (int v : G[u]) {
                    if (--degree[v] == 1) q.push(v);
                }
            }
        }
        while (q.size()) {
            ans.push_back(q.front());
            q.pop();
        }
        return ans;
    }
};
```

</details>

## Build A Matrix With Conditions

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<vector<int>> buildMatrix(int k, vector<vector<int>>& rowConditions, vector<vector<int>>& colConditions) {
        vector<int> order1 = topologicalSort(k, rowConditions);
        vector<int> order2 = topologicalSort(k, colConditions);
        
        if(order1.size() < k || order2.size() < k) return {};
        
        // Mapping of column conditions.
        
        unordered_map<int, int> M;
        for(int i = 0; i < k; i++) {
            M[order2[i]] = i;
        }
        // Create a answer vector and return it.
        vector<vector<int>> ans(k, vector<int>(k, 0));
        for(int i = 0; i < k; i++) {
            ans[i][M[order1[i]]] = order1[i];
        }
        
        return ans;
    }
    
    vector<int> topologicalSort(int k, vector<vector<int>> &A) {
        
        // Degree
        vector<int> deg(k, 0), order;
        
        // Creation of graph
        vector<vector<int>> G(k, vector<int>(0));
        
        for(auto &c : A) {
            int u = c[0], v = c[1];
            G[u - 1].push_back(v - 1);
            deg[v - 1]++;
        }
        
        queue<int> q;
        // Push node with indegree zero.
        
        for(int i = 0; i < k; i++) {
            if(deg[i] == 0) {
                q.push(i);
            }
        }
        
        while(q.size()) {
            int x = q.front();
            q.pop();
            
            order.push_back(x + 1);
            
            for(int &u : G[x]) {
                if(--deg[u] == 0) {
                    q.push(u);
                }
            }
        }
        
        return order;
    }
};
```

</details>

## Longest Increasing Path In Matrix

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int longestIncreasingPath(vector<vector<int>>& A) {
        
        int M = A.size(), N = A[0].size(), dirs[4][2] = {{0,1},{0,-1},{1,0},{-1,0}}, ans = 0;

        vector<vector<int>> indegree(M, vector<int>(N));
        queue<pair<int, int>> q;

        for (int i = 0; i < M; ++i) {
            for (int j = 0; j < N; ++j) {
                for (auto &[dx, dy] : dirs) {
                    int a = i + dx, b = j + dy;
                    if (a < 0 || b < 0 || a >= M || b >= N || A[a][b] >= A[i][j]) continue;
                    indegree[i][j]++;
                }
                if (indegree[i][j] == 0) q.push({ i, j });
            }
        }

        while (q.size()) {
           int cnt = q.size(); 
            ++ans;
            while (cnt--) {
                auto [x, y] = q.front();
                q.pop();
                for (auto &[dx, dy] : dirs) {
                    int a = x + dx, b = y + dy;
                    if (a < 0 || b < 0 || a >= M || b >= N || A[a][b] <= A[x][y]) continue;
                    if (--indegree[a][b] == 0) q.push({ a, b });
                }
            }
        }
        return ans;
    }
};
```

</details>