---
aliases:
  - graph
  - Graph
status: backlog
---

## Related
- [[Source Note File]]
- [[Related Concept Note]]

## 1. Concept
A graph is a data structure denoted by vertices and edges. 

## 2. Mechanics
- 
## 3. Implementation 
- **Adjacency List**
```cpp
using graph = vector<vpii>;

void addEdge(graph& g, int v1, int v2, int w){
    g[v1].pb({v2, w});
    g[v2].pb({v1, w});
}
```

- **Store Edge IDs**
Good for frequent updates

## 4. Terminology
- Multi-edges - two vertices are connected by more than one edge.
- Directed - edges have directions, e.g. from vertex $u$ to vertex $v$, where the opposite is not true.

## References 
- 

