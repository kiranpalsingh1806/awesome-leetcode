## Concatenated Words

```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    bool end = false;
};
class Solution {
    TrieNode root;
    void addWord(TrieNode *node, string &s) {
        for (char c : s) {
            if (!node->next[c - 'a']) node->next[c - 'a'] = new TrieNode();
            node = node->next[c - 'a'];
        }
        node->end = true;
    }
    bool valid(string &s) {
        int N = s.size();
        vector<bool> dp(N + 1);
        dp[0] = true;
        for (int i = 0; i < N && !dp[N]; ++i) {
            if (!dp[i]) continue;
            auto node = &root;
            for (int j = i; j < N - (i == 0); ++j) {
                node = node->next[s[j] - 'a'];
                if (!node) break;
                if (node->end) dp[j + 1] = true;
            }
        }
        return dp[N];
    }
public:
    vector<string> findAllConcatenatedWordsInADict(vector<string>& A) {
        for (auto &s : A) {
            if (s.empty()) continue;
            addWord(&root, s);
        }
        vector<string> ans;
        for (auto &s : A) {
            if (s.size() && valid(s)) ans.push_back(s);
        }
        return ans;
    }
};
```