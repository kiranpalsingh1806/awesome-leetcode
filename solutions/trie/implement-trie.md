## Implement Trie

```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    bool isWord = false;
};

class Trie {
    
    TrieNode root;
    
    TrieNode* find(string s) {
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
        node->isWord = true;
    }
    
    bool search(string word) {
        auto wordFind = find(word);
        return wordFind && wordFind->isWord == true;
    }
    
    bool startsWith(string prefix) {
        return find(prefix);
    }
};
```