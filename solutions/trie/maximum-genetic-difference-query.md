## Maximum Genetic Difference Query

```cpp
struct TrieNode {
    TrieNode *next[2] = {};
    int cnt = 0;
};
class Solution {
public:
    vector<int> maxGeneticDifference(vector<int>& P, vector<vector<int>>& Q) {
        int N = P.size(), M = Q.size(), rootIndex;
        vector<vector<int>> G(N);
        for (int i = 0; i < N; ++i) {
            if (P[i] != -1) G[P[i]].push_back(i);
            else rootIndex = i;
        }
        unordered_map<int, vector<int>> m;
        for (int i = 0; i < M; ++i) m[Q[i][0]].push_back(i);
        TrieNode root;
        auto getAnswer = [&](TrieNode *node, int q) {
            int ans = 0;
            for (int i = 31; i >= 0; --i) {
                int b = q >> i & 1;
                if (node->next[1 - b] && node->next[1 - b]->cnt) {
                    node = node->next[1 - b];
                    ans |= 1 << i;
                } else node = node->next[b];
            }
            return ans;
        };
        vector<int> ans(M);
        function<void(int)> dfs = [&](int u) {
            auto node = &root;
            for (int i = 31; i >= 0; --i) {
                int b = u >> i & 1;
                if (!node->next[b]) node->next[b] = new TrieNode();
                node = node->next[b];
                node->cnt++;
            }
            if (m.count(u)) {
                for (int index : m[u]) ans[index] = getAnswer(&root, Q[index][1]);
            }
            for (int v : G[u]) dfs(v);
            node = &root;
            for (int i = 31; i >= 0; --i) {
                int b = u >> i & 1;
                node = node->next[b];
                node->cnt--;
            }
        };
        dfs(rootIndex);
        return ans;
    }
};
```