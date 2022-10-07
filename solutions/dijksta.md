# Dijkstra's Algorithm

## Network Delay Time

<details>
<summary> View Code </summary>

```cpp
class Solution {
    typedef pair<int, int> PII;
public:
    int networkDelayTime(vector<vector<int>>& E, int n, int k) {
        vector<vector<PII>> G(n);
        for (auto &e : E) G[e[0] - 1].emplace_back(e[1] - 1, e[2]);
        vector<int> dist(n, INT_MAX);
        dist[k - 1] = 0;
        priority_queue<PII, vector<PII>, greater<>> pq;
        pq.emplace(0, k - 1);
        while (pq.size()) {
            auto [cost, u] = pq.top();
            pq.pop();
            if (dist[u] > cost) continue; 
            for (auto &[v, w] : G[u]) {
                if (dist[v] > dist[u] + w) {
                    dist[v] = dist[u] + w;
                    pq.emplace(dist[v], v);
                }
            }
        }
        int ans = *max_element(begin(dist), end(dist));
        return ans == INT_MAX ? -1 : ans;
    }
};
```

</details>

## Cheapest Flights Within K Stops

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        
        // Creation of Graph
        vector<vector<pair<int, int>>> G(n);
        for(auto &e : flights) {
            int u = e[0], v = e[1], w = e[2];
            G[u].push_back({v, w});
        }
        
        k++;
        
        // Cost, CityID, Stops left
        priority_queue<array<int, 3>, vector<array<int, 3>>, greater<>> pq;
        pq.push({0, src, k});
        
        //Minimum distance
        vector<vector<int>> dist(k + 1, vector<int>(n, INT_MAX));
        
        for (int i = 0; i <= k; i++) {
            dist[i][src] = 0;
        }
        
        while (pq.size()) {
            auto [c, u, stop] = pq.top();
            pq.pop();
            
            if (c > dist[stop][u]) continue;
            if (u == dst) return c;
            if (stop == 0) continue;
            
            for (auto &[v, w] : G[u]) {
                int newCost = c + w;
                if (dist[stop - 1][v] > newCost) {
                    dist[stop - 1][v] = newCost;
                    pq.push({newCost, v, stop - 1});
                }
            } 
        }
        
        return -1;
    }
};
```

</details>

## Path With Minimum Effort

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    
    int dirs[4][2] = { {0, 1}, {1, 0}, {-1, 0}, {0, -1}};
    
    int minimumEffortPath(vector<vector<int>>& A) {
        
        int M = A.size(), N = A[0].size();
        
        vector<vector<int>> dist(M, vector<int>(N, INT_MAX));
        priority_queue<array<int, 3>, vector<array<int, 3>>, greater<>> pq;
        pq.push({0, 0, 0});
        dist[0][0] = 0;
        
        while (pq.size()) {
            auto [cost, a, b] = pq.top();
            pq.pop();
            
            if (cost > dist[a][b]) continue;
            if (a == M - 1 && b == N - 1) return cost;
            
            for(auto &dir : dirs) {
                int x = a + dir[0];
                int y = b + dir[1];
                
                if (x < 0 || y < 0 || x >= M || y >= N) continue;
                
                int newCost = max(cost, abs(A[a][b] - A[x][y]));
                
                if (newCost < dist[x][y]) {
                    dist[x][y] = newCost;
                    pq.push({newCost, x, y});
                }
            }
        }
        
        return dist[M - 1][N - 1];
    }
};
```

</details>

## Minimum Cost To Make Atleast One Valid Path In Graph

<details>
<summary> View Code </summary>

```cpp
class Solution {
public:
    int dirs[4][2] = {{0, 1}, {0, -1}, {1, 0}, {-1, 0}};
    int minCost(vector<vector<int>>& grid) {
        int M = grid.size(), N = grid[0].size();
        
        int dist[100][100] = {};
        memset(dist, 0x3f, sizeof(dist));
        
        // Cost, X, Y
        priority_queue<array<int, 3>, vector<array<int, 3>>, greater<>> pq;
        pq.push({0, 0, 0});
        dist[0][0] = 0;
        
        while (pq.size()) {
            auto [cost, x, y] = pq.top();
            pq.pop();
            
            if (cost > dist[x][y]) continue;
            if (x == M - 1 && y == N - 1) return cost;
            
            for (int i = 0; i < 4; i++) {
                int a = x + dirs[i][0];
                int b = y + dirs[i][1];
                
                if (a < 0 || b < 0 || a >= M || b >= N) continue;
                
                int newCost = cost + (grid[x][y] != i + 1);
                
                if (dist[a][b] > newCost) {
                    dist[a][b] = newCost;
                    pq.push({newCost, a, b});
                }
            }
        }
        
        return 0;
    }
};
```

</details>