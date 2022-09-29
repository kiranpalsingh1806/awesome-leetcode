# Bellman Ford Algorithm

## Cheapest Flights Within K Stops

```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) {
        vector<int> dist(n, 1e9);
        
        dist[src] = 0; 
        
        // K relaxation
        
        for(int i = 0; i <= k; i++) {
            auto temp = dist;
            
            for(auto &e : flights) {
                int u = e[0], v = e[1], w = e[2];
                
                dist[v] = min(dist[v], temp[u] + w);
            }
        }
        
        if(dist[dst] == 1e9) {
            return -1;
        } else {
            return dist[dst];
        }
    }
};
```

## Network Delay Time

```cpp
class Solution {
public:
    int networkDelayTime(vector<vector<int>>& times, int n, int k) {
        vector<int> dist(n, 1e9);
        
        dist[k - 1] = 0;
        
        for(int i = 0; i < n; i++) {
            
            for(auto &e : times) {
                int u = e[0] - 1, v = e[1] - 1, w = e[2];
                if(dist[u] != 1e9) {
                    dist[v] = min(dist[v], dist[u] + w);
                }   
            }
        }
        
        int answer = *max_element(dist.begin(), dist.end());
        
        if(answer == 1e9) {
            return -1;
        } else {
            return answer;
        }
    }
};
```