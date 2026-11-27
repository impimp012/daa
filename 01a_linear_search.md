# Experiment 1(a): Linear Search
**Date:** 4/8/25 | **Page No.:** 2

## Aim
Design and analysis of linear search algorithm.

## Algorithm
```
LinearSearch(target, n, arr[]):
    i = 0;                      -> 1
    while i < n:                -> n+1
        if arr[i] == target:    -> n
            return i;           -> 1 (once, if found)
        i++;                    -> n
    return -1;                  -> 1
```

## Time Complexity
```
T(n) = 1 + (1+1+1)n + 1
     = 3n + 2
     = O(n)
```
Linear search has time complexity **O(n)** and space complexity **O(1)**.
Best case O(1), worst case O(n), average O(n).

## Code
```cpp
#include <iostream>
using namespace std;

int main() {
    cout << "Shivansh Kumar\nCSE C\n12220802723\n";

    int arr[] = {10, 25, 30, 45, 50};
    int n = sizeof(arr) / sizeof(arr[0]);
    int key;
    cin >> key;
    for (int i = 0; i < n; i++) {
        if (arr[i] == key) {
            cout << "Element found at index " << i;
            return 0;
        }
    }
    cout << "Element not found";
    return 0;
}
```

## Output
```
Shivansh Kumar
CSE C
12220802723
45
Element found at index 3
```
