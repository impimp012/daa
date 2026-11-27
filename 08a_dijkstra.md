# Experiment 8(a): Dijkstra's Algorithm
**Page No.:** 18

## Aim
Design and analysis of Dijkstra's algorithm.

## Algorithm
- Assume no negative-weight edges.
- Maintains a set of vertices whose shortest path (SP) from source s has been determined.
- Repeatedly selects u in V-S with minimum SP estimate.
- Store V-S in priority queue Q.

```
Initialise(G, s);
S := empty;
Q := V[G];
while Q != empty do
    u := Extract-Min(Q);            -> V log V
    S := S U {u};
    for each v in Adj[u] do
        Relax(u, v, w)              -> E log V
    od
od

Relax(u, v, w):
    if d[v] > d[u] + w(u,v) then
        d[v] := d[u] + w(u,v);
        pi[v] := u
```

## Time Complexity
```
T(n) = O(V log V) + O(E log V)
     = O((V+E) log V)
```

## Code
> Lines 1-26 of the program are missing from your file (pasted pages start at line 27). They are reconstructed below to match the visible lines 27-74.

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>
using namespace std;

struct Edge {
    int to, weight;
};

void dijkstra(int start, const vector<vector<Edge>>& graph) {
    int n = graph.size();
    vector<int> dist(n, INT_MAX);
    priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;

    dist[start] = 0;
    pq.push({0, start});

    while (!pq.empty()) {
        int currDist = pq.top().first;
        int node = pq.top().second;
        pq.pop();

        // If this distance is outdated, skip it
        if (currDist > dist[node]) continue;

        // Explore all neighbors
        for (auto edge : graph[node]) {
            int nextNode = edge.to;
            int newDist = currDist + edge.weight;

            if (newDist < dist[nextNode]) {
                dist[nextNode] = newDist;
                pq.push({newDist, nextNode});
            }
        }
    }

    // Print the shortest distances
    cout << "Shortest distances from node " << start << ":\n";
    for (int i = 0; i < n; ++i) {
        if (dist[i] == INT_MAX)
            cout << "Node " << i << " is unreachable\n";
        else
            cout << "Node " << i << " -> " << dist[i] << "\n";
    }
}

int main() {
    int vertices, edges;

    cout << "Enter number of vertices and edges: ";
    cin >> vertices >> edges;

    vector<vector<Edge>> graph(vertices);

    cout << "Enter edges (u v w):\n";
    for (int i = 0; i < edges; ++i) {
        int u, v, w;
        cin >> u >> v >> w;
        graph[u].push_back({v, w});
        graph[v].push_back({u, w}); // Remove this line for directed graph
    }

    int start;
    cout << "Enter starting node: ";
    cin >> start;

    dijkstra(start, graph);

    return 0;
}
```

## Output
Output screenshot for Dijkstra is not in your file. Sample (run it and paste your own):
```
Enter number of vertices and edges: 5 6
Enter edges (u v w):
0 1 2
0 2 4
1 2 1
1 3 7
2 4 3
3 4 2
Enter starting node: 0
Shortest distances from node 0:
Node 0 -> 0
Node 1 -> 2
Node 2 -> 3
Node 3 -> 8
Node 4 -> 6
```
