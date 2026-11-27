# Experiment 6(b): Kruskal's Algorithm for Minimum Spanning Tree
**Date:** 1/9/25 | **Page No.:** 15

## Aim
Design and analysis of Kruskal's algorithm for minimum spanning tree.

## Algorithm
```
Kruskal(G, E):
    for each vertex v in V:
        MakeSet(v)
    sort all edges in increasing order of weight      -> O(E log E)
    MST = empty set
    for each edge (u,v) in sorted order:              -> O(E)
        if FindSet(u) != FindSet(v):
            add edge (u,v) to MST
            Union(u,v)
        if MST has (V-1) edges:
            break
    Print MST edges
```

## Time Complexity
```
T(n) = O(E) + O(E log E)
     = O(E log E) ~ O(E log V)   for connected graph
```

## Code
```cpp
#include <iostream>
#include <algorithm>
using namespace std;

struct Edge {
    int u, v, weight;
};
bool compare(Edge a, Edge b) {
    return a.weight < b.weight;
}
class DisjointSet {
    int *parent, *rank;
public:
    DisjointSet(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            rank[i] = 0;
        }
    }
    int find(int x) {
        if (parent[x] != x)
            parent[x] = find(parent[x]);
        return parent[x];
    }
    bool unite(int x, int y) {
        int xr = find(x), yr = find(y);
        if (xr == yr) return false;
        if (rank[xr] < rank[yr])
            parent[xr] = yr;
        else if (rank[xr] > rank[yr])
            parent[yr] = xr;
        else {
            parent[yr] = xr;
            rank[xr]++;
        }
        return true;
    }
};

int main() {
    cout << "Shivansh Kumar   CSE-C\n12220802723\n";
    int V, E;
    cout << "Enter number of vertices and edges: ";
    cin >> V >> E;
    Edge *edges = new Edge[E];
    cout << "Enter edges (u v weight) [0-based index]:\n";
    for (int i = 0; i < E; i++) {
        cin >> edges[i].u >> edges[i].v >> edges[i].weight;
    }
    sort(edges, edges + E, compare);
    DisjointSet ds(V);
    int mst_weight = 0;
    cout << "Edges in the Minimum Spanning Tree:\n";
    for (int i = 0; i < E; i++) {
        if (ds.unite(edges[i].u, edges[i].v)) {
            cout << edges[i].u << " - " << edges[i].v
                 << " : " << edges[i].weight << "\n";
            mst_weight += edges[i].weight;
        }
    }
    cout << "Total weight of MST: " << mst_weight << endl;
    delete[] edges;
    return 0;
}
```

## Output
```
Shivansh Kumar   CSE-C
12220802723
Enter number of vertices and edges: 4 5
Enter edges (u v weight) [0-based index]:
0 1 10
0 2 8
0 3 6
1 2 20
2 3 10
Edges in the Minimum Spanning Tree:
0 - 3 : 6
0 - 2 : 8
0 - 1 : 10
Total weight of MST: 24
```
