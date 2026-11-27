# Experiment 3: Quick Sort
**Date:** 18/8/25 | **Page No.:** 8-9

## Aim
Design and analysis of quick sorting algorithm.

## Algorithm
```
Quicksort(arr, low, high)
    if low < high
        p = Partition(arr, low, high)
        Quicksort(arr, low, p-1)
        Quicksort(arr, p+1, high)

Partition(arr, low, high)
    pivot = arr[high]
    i = low - 1
    for j = low to high-1
        if arr[j] <= pivot
            i = i+1
            Swap arr[i], arr[j]
    Swap arr[i+1], arr[high]
    return i+1
```

## Time Complexity
### i) Best / average case
```
T(n)   = T(n/2) + T(n/2) + n = 2T(n/2) + n
T(n/2) = 2T(n/4) + n/2
T(n/4) = 2T(n/8) + n/4
T(n)   = 2(2T(n/4) + n/2) + n = 4T(n/4) + 2n
       = 8T(n/8) + 3n  =>  T(n) = 2^k T(n/2^k) + kn
Let n/2^k = 1 => n = 2^k => k = log n
T(n) = nT(1) + n log n = n + n log n  =>  O(n log n)
```
### ii) Worst case (sorted array)
```
T(n)   = T(n-1) + n
T(n-1) = T(n-2) + (n-1)
T(n-2) = T(n-3) + (n-2)
T(n)   = T(n-3) + n-2 + 2n-1 = T(n-3) + 3n - 3
T(n)   = T(n-k) + kn - k,   n-k = 1 => k = n-1
T(n)   = T(1) + (n-1)n - (n-1) = n^2 - 2n - 1  =>  O(n^2)
```
Space: O(log n) average stack, O(n) worst.

## Code
```cpp
#include <iostream>
using namespace std;

int partition(int arr[], int low, int high) {
    int pivot = arr[high];
    int i = (low - 1);
    for (int j = low; j < high; j++) {
        if (arr[j] < pivot) {
            i++;
            swap(arr[i], arr[j]);
        }
    }
    swap(arr[i + 1], arr[high]);
    return (i + 1);
}

void quickSort(int arr[], int low, int high) {
    if (low < high) {
        int partitionIndex = partition(arr, low, high);
        quickSort(arr, low, partitionIndex - 1);
        quickSort(arr, partitionIndex + 1, high);
    }
}

int main() {
    cout << "Shivansh Kumar \tCSE-C\n12220802723" << endl;
    int arr[] = {12, 7, 10, 11, 4, 6};
    int n = sizeof(arr) / sizeof(arr[0]);
    quickSort(arr, 0, n - 1);
    cout << "Sorted array: ";
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";
    cout << endl;
    return 0;
}
```
> The last lines of `main` (after the array declaration) are cut off in your file; they are completed here to match your output.

## Output
```
Shivansh Kumar  CSE-C
12220802723
Sorted array: 4 6 7 10 11 12
```
