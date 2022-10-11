## Sum of Prefix Scores of Strings

```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    int cnt = 0;
};

class Solution {
    TrieNode root;
public:
    void insert(string word) {
        auto node = &root;
        for(char c : word) {
            if(!node->next[c - 'a']) {
                node->next[c - 'a'] = new TrieNode();
            } 
            node->next[c - 'a']->cnt++;
            node = node->next[c - 'a'];   
        }
    }

    int prefixCnt(string s) {
        auto node = &root;
        int ans = 0;
        for(char c : s) {
            ans += node->next[c - 'a']->cnt;
            node = node->next[c - 'a'];
        }
        return ans;
    }
    
    vector<int> sumPrefixScores(vector<string>& words) {
        int N = words.size();
		// Insert words in trie.
        for (int i = 0; i < N; i++) {
                insert(words[i]);
        }
        vector<int> ans(N, 0);
        for (int i = 0; i < N; i++) {
			// Get the count of all prefixes of given string.
            ans[i] = prefixCnt(words[i]); 
        }
        return ans;
    }
};
```