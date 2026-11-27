# Experiment 2(c): Bubble Sort
**Date:** 11/8/25 | **Page No.:** 7

## Aim
Design and analysis of bubble sorting algorithm.

## Algorithm
```
BubbleSort(arr):
    n = length(arr)                          -> 1
    for i = 0 to n-2:                        -> n-1
        for j = 0 to n-i-2:                  -> (n-1)(n-2)
            if arr[j] > arr[j+1]:            -> (n-1)^2
                Swap(arr[j], arr[j+1])
```

## Time Complexity
```
T(n) = 1 + n-1 + n^2 - 2n - n + 2 + n^2 - 2n + 1
     = 2n^2 - 4n + 3
     = O(n^2)
```
Bubble sort has time complexity **O(n^2)** and space complexity **O(1)**.

## Code
> Note: the printed code for bubble sort is not in your file (only the algorithm and complexity page). The program below is the standard implementation of the same algorithm, in the same format as your other experiments. Run it once and paste your own screenshot.

```cpp
#include <iostream>
using namespace std;

int main() {
    cout<<"Shivansh Kumar\nCSE-C\n12220802723\n";
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);

    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (arr[j] > arr[j + 1])
                swap(arr[j], arr[j + 1]);
        }
    }

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```

## Output (expected)
```
Shivansh Kumar
CSE-C
12220802723
11 12 22 25 34 64 90
```
