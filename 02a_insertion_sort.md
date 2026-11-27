# Experiment 2(a): Insertion Sort
**Date:** 11/8/25 | **Page No.:** 5

## Aim
Design and analysis of insertion sorting algorithm.

## Algorithm
```
InsertionSort(arr):
    n = length(arr)                          -> 1
    for i = 1 to n-1:                        -> n
        key = arr[i]                         -> n-1
        j = i-1                              -> n-1
        while j >= 0 and arr[j] > key:       -> n(n-1)
            arr[j+1] = arr[j]                -> n^2
            j = j-1                          -> n^2
        arr[j+1] = key                       -> (n-1)
```

## Time Complexity
```
T(n) = 1 + n + (n-1) + (n-1) + (n^2-n) + n^2 + n^2 + (n-1)
     = 3n^2 + 3n - 2
     = O(n^2)
```
Insertion sort has time complexity **O(n^2)** and space complexity **O(1)**.
(Best case O(n) when already sorted.)

## Code
```cpp
#include <iostream>
using namespace std;

int main() {
    cout<<"Shivansh Kumar\nCSE-C\n12220802723\n";

    int arr[] = {12, 11, 13, 5, 6};
    int n = sizeof(arr) / sizeof(arr[0]);

    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j = j - 1;
        }
        arr[j + 1] = key;
    }

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;

    return 0;
}
```

## Output
```
Shivansh Kumar
CSE-C
12220802723
5 6 11 12 13
```
