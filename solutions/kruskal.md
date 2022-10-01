# Kruskal Algorithm

## Min Cost To Connect All Points

<details>
<summary> View Code </summary>

```cpp
class UnionFind {
    private:
        vector<int> id, rank;
        int cnt;
    public:
        UnionFind(int cnt) : cnt(cnt) {
            id = vector<int>(cnt);
            rank = vector<int>(cnt, 0);
            for (int i = 0; i < cnt; ++i) id[i] = i;
        }
        int find(int p) {
            if (id[p] == p) return p;
            return id[p] = find(id[p]);
        }
        int getCount() { 
            return cnt; 
        }
        bool connected(int p, int q) { 
            return find(p) == find(q); 
        }
        void connect(int p, int q) {
            int i = find(p), j = find(q);
            if (i == j) return;
            if (rank[i] < rank[j]) {
                id[i] = j;  
            } else {
                id[j] = i;
                if (rank[i] == rank[j]) rank[j]++;
            }
            --cnt;
        }
};

class Solution {
public:
    int minCostConnectPoints(vector<vector<int>>& points) {
        
        int N = points.size();
        
        vector<array<int, 3>> E;
        
        for(int i = 0; i < N; i++) {
            for(int j = i + 1; j < N; j++) {
                E.push_back({abs(points[i][0] - points[j][0]) + abs(points[i][1] - points[j][1]), i, j});
            }
        }
        
        UnionFind uf(N);
        
        int ans = 0;
        
        // How to convert vector into heap.
        make_heap(E.begin(), E.end(), greater<array<int, 3>>());
        
        while(uf.getCount() > 1) {
            pop_heap(E.begin(), E.end(), greater<array<int, 3>>());
            auto [w, u, v] = E.back();
            
            E.pop_back();
            
            if(uf.connected(u, v)) continue;
            
            uf.connect(u, v);
            ans += w;
        }
        
        return ans;
        
    }
};
```
</details>


## Find Critical and Pseudo-Critical Edges in Minimum Spanning Tree

<details>
<summary> View Code </summary>

```cpp
class UnionFind {
    vector<int> id;
    int size;
public:
    UnionFind(int N) : id(N), size(N) {
        iota(begin(id), end(id), 0);
    }
    int find(int x) {
        return id[x] == x ? x : (id[x] = find(id[x]));
    }
    bool connect(int x, int y) {
        int p = find(x), q = find(y);
        if (p == q) return false;
        id[p] = q;
        --size;
        return true;
    }
    int getSize() { return size; }
};
class Solution {
    int kruskal(int n, vector<vector<int>> &E, int include = -1, int exclude = -1) {
        int cost = 0;
        UnionFind uf(n);
        if (include != -1) {
            auto &e = E[include];
            uf.connect(e[0], e[1]);
            cost += e[2];
        }
        for (int i = 0; i < E.size(); ++i) {
            if (i == include || i == exclude) continue;
            int u = E[i][0], v = E[i][1], w = E[i][2], id = E[i][3];
            if (!uf.connect(u, v)) continue;
            cost += w;
            if (uf.getSize() == 1) break;
        }
        return uf.getSize() == 1 ? cost : INT_MAX;
    }
public:
    vector<vector<int>> findCriticalAndPseudoCriticalEdges(int n, vector<vector<int>>& E) {
        for (int i = 0; i < E.size(); ++i) E[i].push_back(i);
        sort(begin(E), end(E), [](vector<int> &a, vector<int> &b) { return a[2] < b[2]; });
        int cost = kruskal(n, E);        
        vector<int> c, p;
        for (int i = 0; i < E.size(); ++i) {
            if (kruskal(n, E, -1, i) > cost) c.push_back(E[i][3]);
            else if (kruskal(n, E, i) == cost) p.push_back(E[i][3]);
        }
        return { c, p };
    }
};
```

</details>