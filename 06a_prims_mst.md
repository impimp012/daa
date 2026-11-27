# Experiment 6(a): Prim's Algorithm for Minimum Spanning Tree
**Date:** 1/9/25 | **Page No.:** 14

## Aim
Design and analysis of Prim's algorithm for minimum spanning tree.

## Algorithm
```
Prim(G, V):                                     -> O(V) for initialisation
    for each vertex u in V:
        key[u] = infinity
        parent[u] = -1
        inMST[u] = false
    key[0] = 0
    repeat (V-1) times:                         -> O(V log V)
        u = vertex with minimum key[] not in MST
        inMST[u] = true
        for each vertex v adjacent to u:        -> O(E log V)
            if (v not in MST) AND (weight(u,v) < key[v]):
                parent[v] = u
                key[v] = weight(u,v)
    Print parent[] and key[]  -> MST edges     -> O(V)
```

## Time Complexity
```
T(n) = O(V) + O(V log V) + O(E log V)
     = O((E+V) log V)        (binary heap / adjacency list)
```
The matrix-based code below (linear scan for the minimum) runs in O(V^2). Space O(V).

## Code
```cpp
#include <iostream>
#include <climits>
using namespace std;
#define MAX 100

int findMinKey(int key[], bool mstSet[], int V) {
    int min = INT_MAX, min_index = -1;
    for (int v = 0; v < V; v++) {
        if (!mstSet[v] && key[v] < min) {
            min = key[v];
            min_index = v;
        }
    }
    return min_index;
}

void primMST(int graph[MAX][MAX], int V) {
    int parent[MAX];
    int key[MAX];
    bool mstSet[MAX];
    for (int i = 0; i < V; i++) {
        key[i] = INT_MAX;
        mstSet[i] = false;
    }
    key[0] = 0;
    parent[0] = -1;
    for (int count = 0; count < V - 1; count++) {
        int u = findMinKey(key, mstSet, V);
        mstSet[u] = true;

        for (int v = 0; v < V; v++) {
            if (graph[u][v] && !mstSet[v] && graph[u][v] < key[v]) {
                parent[v] = u;
                key[v] = graph[u][v];
            }
        }
    }
    cout << "Edges in the Minimum Spanning Tree:\n";
    int totalWeight = 0;
    for (int i = 1; i < V; i++) {
        cout << parent[i] << " - " << i << " : " << graph[i][parent[i]] << "\n";
        totalWeight += graph[i][parent[i]];
    }
    cout << "Total weight of MST: " << totalWeight << endl;
}

int main() {
    cout << "Shivansh Kumar   CSE-C\n12220802723\n";
    int V;
    cout << "Enter number of vertices: ";
    cin >> V;
    int graph[MAX][MAX];
    cout << "Enter adjacency matrix (0 if no edge):\n";
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            cin >> graph[i][j];
        }
    }
    primMST(graph, V);
    return 0;
}
```

## Output
```
Shivansh Kumar   CSE-C
12220802723
Enter number of vertices: 5
Enter adjacency matrix (0 if no edge):
0 2 0 6 0
2 0 3 8 5
0 3 0 0 7
6 8 0 0 9
0 5 7 9 0
Edges in the Minimum Spanning Tree:
0 - 1 : 2
1 - 2 : 3
0 - 3 : 6
1 - 4 : 5
Total weight of MST: 16
```
