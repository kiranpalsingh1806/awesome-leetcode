## Search Suggestion System

```cpp
struct TrieNode {
    TrieNode *next[26] = {};
    int index = -1;
};

void add(TrieNode *node, string &product, int i) {
    for(char c : product) {
        if(!node->next[c - 'a']) node->next[c - 'a'] = new TrieNode();
        node = node->next[c - 'a'];
    }
    node->index = i;
}

void collect(TrieNode* node, vector<string> &ans, vector<string> &products) {
    
    if(ans.size() == 3) return;
    
    if(!node) return;
    
    if(node->index > -1) ans.push_back(products[node->index]);
    
    for(int i = 0; i < 26; i++) {
        // Starting three valid words -> add them into answer -> return the function.
        if(node->next[i]) {
            collect(node->next[i], ans, products);
        }
    }
}

class Solution {
public:
    vector<vector<string>> suggestedProducts(vector<string>& products, string searchWord) {
        TrieNode root, *node = &root;
        
        int N = products.size();
        
        vector<vector<string>> ans(searchWord.length());
        
        for(int i = 0; i < N; i++) {
            add(&root, products[i], i);
        }
        
        for(int i = 0; i < searchWord.length(); i++) {
            node = node->next[searchWord[i] - 'a'];
            
            if(!node) break;
            
            // Collect three words from dictionary as per lexicographical order
            collect(node, ans[i], products);
        }
        
        return ans;
    }
};
```