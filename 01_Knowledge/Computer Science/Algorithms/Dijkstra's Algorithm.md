---
aliases:
  - Dijkstra
  - dijkstra
status: complete
tags:
  - graph/shortest-path
  - algo/greedy
---
**Prerequisites**
- [[Basic - Graph|Graph]]

## 1. Quick Summary 
A greedy shortest path algorithm for weighted graphs that works by picking the immediate cheapest neighbor at each step. Dijkstra can calculate the shortest path from one point to all other points.

**Time Complexity**
- 
**Space Complexity**
- 

## 2. Core Concepts & Mechanics
**Steps**
- Keep a list of visited and unvisited notes.
- Assign tentative values to all points, from point A assign 0, $\infty$ to every other points.
- For current node, calculate distance to all unvisited neighbours, and update the the distance values accordingly, if the value is less than previous value.
- Move to the neighbour with shortest distance
- Repeat for the next node, but this time use the cumulative sum of the distance (total distance from A to the next)

**Limitations**
- Negative weights
- Unoptimal for unweighted
- Mutable weights

## 3. Implementation 

```cpp
vector<int> dijkstra(vector<vector<pair<int,int>>>& adj, int src) {
    int V = adj.size();

    // Min-heap (priority queue) storing pairs of (distance, node)
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    vector<int> dist(V, INT_MAX);

    // Distance from source to itself is 0
    dist[src] = 0;
    pq.emplace(0, src);

    // Process the queue until all reachable vertices are finalized
    while (!pq.empty()) {
        auto top = pq.top();
        pq.pop();

        int d = top.first;  
        int u = top.second; 

        // If this distance not the latest shortest one, skip it
        if (d > dist[u])
            continue;

        // Explore all neighbors of the current vertex
        for (auto &p : adj[u]) {
            int v = p.first; 
            int w = p.second; 

            // If we found a shorter path to v through u, update it
            if (dist[u] + w < dist[v]) {
                dist[v] = dist[u] + w;   
                pq.emplace(dist[v], v);
            }
        }
    }

    // Return the final shortest distances from the source
    return dist;
}
```
## References 
- https://www.geeksforgeeks.org/dsa/dijkstras-shortest-path-algorithm-greedy-algo-7/

