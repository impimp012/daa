# Experiment 2(b): Selection Sort
**Date:** 11/8/25 | **Page No.:** 6

## Aim
Design and analysis of selection sorting algorithm.

## Algorithm
```
SelectionSort(arr):
    n = length(arr)                          -> 1
    for i = 0 to n-2:                        -> n-1
        minIndex = i                         -> n-2
        for j = i+1 to n-1:                  -> (n-1)^2
            if arr[j] < arr[minIndex]        -> (n-1)(n-2)
                minIndex = j                 -> (n-1)(n-1)
        Swap(arr[i], arr[minIndex])          -> (n-1)
```

## Time Complexity
```
T(n) = 1 + n-1 + n-2 + (n-1)^2 + (n-1)(n-2) + (n-1)(n-1) + (n-1)
     = 3n^2 - 4n + 1
     = O(n^2)
```
Selection sort has time complexity **O(n^2)** and space complexity **O(1)**.
(Best, average and worst case are all O(n^2); only n-1 swaps.)

## Code
```cpp
#include <iostream>
using namespace std;

int main() {
    //Selection Sort
    cout<<"Shivansh Kumar\nCSE-C\n12220802723\n";
    int arr[] = {29, 10, 14, 37, 13};
    int n = sizeof(arr) / sizeof(arr[0]);

    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (arr[j] < arr[minIndex])
                minIndex = j;
        }
        swap(arr[minIndex], arr[i]);
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
10 13 14 29 37
```
