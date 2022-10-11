## Maximum XOR of Two Numbers In An Array

```cpp
struct TrieNode {
    TrieNode *next[2] = {};
};
class Solution {
    void add(TrieNode *node, int n) {
        for (int i = 31; i >= 0; --i) {
            int b = n >> i & 1;
            if (node->next[b] == NULL) node->next[b] = new TrieNode();
            node = node->next[b];
        }
    }
    int maxXor(TrieNode *node, int n) {
        int ans = 0;
        for (int i = 31; i >= 0; --i) {
            int b = n >> i & 1;
            if (node->next[1 - b]) { // if we can go the opposite direction, do it.
                node = node->next[1 - b];
                ans |= 1 << i;
            } else {
                node = node->next[b];
            }
        }
        return ans;
    }
public:
    int findMaximumXOR(vector<int>& A) {
        TrieNode root;
        int ans = 0;
        for (int n : A) {
            add(&root, n);
            ans = max(ans, maxXor(&root, n));
        }
        return ans;
    }
};
```