# Experiment 1(b): Binary Search
**Date:** 4/8/25 | **Page No.:** 3-4

## Aim
Design and analysis of binary search algorithm.

## Algorithm
```
BinarySearch(target, n, arr[]):
    low = 0                          -> 1
    high = n-1                       -> 1
    while low <= high:               -> log n
        mid = low + (high-low)/2     -> 1
        if arr[mid] == target:       -> 1
            return mid;              -> 1
        else if arr[mid] < target:
            low = mid+1;             -> 1
        else
            high = mid-1;            -> 1
    return -1;
```
**Initial condition:** the array must be sorted.

## Time Complexity
```
T(n)   = T(n/2) + c
T(n/2) = T(n/4) + c      T(n/4) = T(n/8) + c
T(n)   = T(n/8) + 3c = T(n/2^3) + 3c = T(n/2^k) + kc

Series terminates when n/2^k = 1  =>  2^k = n  =>  k = log2 n
T(n) = T(1) + c log2 n
T(n) = c log2 n
T(n) = O(log2 n)
```
Line-by-line: T(n) = 1+1+log n+1+1+1 = 5 + log n = O(log n).

Binary search takes **O(log n)** time (array sorted) and **O(1)** space.

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
    int low = 0, high = n - 1;
    while (low <= high) {
        int mid = low + (high - low) / 2;
        if (arr[mid] == key) {
            cout << "Element found at index " << mid;
            return 0;
        }
        else if (arr[mid] < key) {
            low = mid + 1;
        }
        else {
            high = mid - 1;
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
50
Element found at index 4
```
