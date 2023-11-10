# DFS

## 13. Restore the Array From Adjacent Pairs

```cpp
class Solution {
public:
    unordered_map<int, vector<int>> graph;

    vector<int> restoreArray(vector<vector<int>>& adjacentPairs) {
        for (auto &edge: adjacentPairs) {
            graph[edge[0]].push_back(edge[1]);
            graph[edge[1]].push_back(edge[0]);
        }

        int root = 0;
        for (auto &[a, b] : graph) {
            if (b.size() == 1) {
                root = a;
            }
        }

        vector<int> ans;
        dfs(root, INT_MAX, ans);
        return ans;
    }

    void dfs(int start, int prev, vector<int>&ans) {
        ans.push_back(start);
        for (int neighbours: graph[start]) {
            if (neighbours != prev) {
                dfs(neighbours, start, ans);
            }
        }
    }
};
```
