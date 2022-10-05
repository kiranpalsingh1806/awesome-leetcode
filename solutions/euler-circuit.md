# Euler Circuit

## Reconstruct Itinerary

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    vector<string> findItinerary(vector<vector<string>>& E) {
        unordered_map<string, multiset<string>> G;
        for (auto &e : E) G[e[0]].insert(e[1]);
        vector<string> ans;
        function<void(string)> euler = [&](string u) {
            while (G[u].size()) {
                auto v = *G[u].begin();
                G[u].erase(G[u].begin());
                euler(v);
            }
            ans.push_back(u);
        };
        euler("JFK");
        return vector<string>(rbegin(ans), rend(ans));
    }
};
```

</details>

## Cracking The Safe

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    string crackSafe(int n, int k) {
        
        if(n == 1 && k == 1) return "0";
        unordered_set<string> M; 
        
        string start = string(n - 1, '0');
        string ans = "";
        
        function<void(string)> euler = [&](string u) {      
            for(char c = '0'; c < k + '0'; c++) {
                string v = u + c;
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

</details>

## Valid Arrangement of Pairs

<details>
<summary> View Code </summary>

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

</details>