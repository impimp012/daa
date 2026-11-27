# Experiment 8(b): Bellman-Ford Algorithm
**Page No.:** 19

## Aim
Design and analysis of Bellman-Ford's algorithm.

## Algorithm
Can have negative weight edges.
```
Initialise(G, s);
for i := 1 to |V[G]| - 1 do
    for each (u,v) in E[G] do
        Relax(u, v, w)
    od
od;
for each (u,v) in E[G] do
    if d[v] > d[u] + w(u,v) then
        return false
    fi
od;
return true;
```

## Time Complexity (as written in your file)
```
O(V^2)          using linear array for priority queue
O((V+E) log V)  using binary heap
O(V log V + E)  using fibonacci heap
```
> Note for viva: these are the Dijkstra-style bounds. The standard time complexity of Bellman-Ford itself is **O(V * E)** (V-1 passes over all E edges), space O(V).

## Code
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

// Structure to represent an edge
struct Edge {
    int from, to, weight;
};

// Bellman-Ford algorithm function
void bellmanFord(int vertices, int start, const vector<Edge>& edges)
{
    vector<int> dist(vertices, INT_MAX);
    dist[start] = 0;

    // Step 1: Relax all edges |V| - 1 times
    for (int i = 1; i < vertices; ++i) {
        for (auto e : edges) {
            if (dist[e.from] != INT_MAX && dist[e.from] + e.weight < dist[e.to]) {
                dist[e.to] = dist[e.from] + e.weight;
            }
        }
    }

    // Step 2: Check for negative weight cycles
    for (auto e : edges) {
        if (dist[e.from] != INT_MAX && dist[e.from] + e.weight < dist[e.to]) {
            cout << "Graph contains a negative weight cycle!\n";
            return;
        }
    }

    // Step 3: Print shortest distances
    cout << "\nShortest distances from node " << start << ":\n";
    for (int i = 0; i < vertices; ++i) {
        if (dist[i] == INT_MAX)
            cout << "Node " << i << " is unreachable\n";
        else
            cout << "Node " << i << " -> " << dist[i] << "\n";
    }
}

int main() {
    int vertices, edgesCount;
    cout << "Enter number of vertices and edges: ";
    cin >> vertices >> edgesCount;

    vector<Edge> edges;

    cout << "Enter edges in format (u v w):\n";
    cout << "(u = from, v = to, w = weight)\n";
    for (int i = 0; i < edgesCount; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        edges.push_back({u, v, w});
    }

    int start;
    cout << "Enter starting node: ";
    cin >> start;

    bellmanFord(vertices, start, edges);

    return 0;
}
```

## Output
```
Enter number of vertices and edges: 5 8
Enter edges in format (u v w):
(u = from, v = to, w = weight)
0 1 4
1 2 4
1 4 5
0 4 3
4 3 2
0 2 7
3 2 -4
2 1 -3
Enter starting node: 0

Shortest distances from node 0:
Node 0 -> 0
Node 1 -> -2
Node 2 -> 1
Node 3 -> 5
Node 4 -> 3
```
