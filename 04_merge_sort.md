# Experiment 4: Merge Sort
**Date:** 25/8/25 | **Page No.:** 10-12

## Aim
Design and analysis of merge sorting algorithm.

## Algorithm
```
MergeSort(A, left, right):
    if left >= right:
        return
    mid = (left + right) / 2
    MergeSort(A, left, mid)
    MergeSort(A, mid+1, right)
    Merge(A, left, mid, right)

Merge(A, left, mid, right):
    n1 = mid - left + 1
    n2 = right - mid
    create arrays L[1..n1], R[1..n2]
    for i from 1 to n1: L[i] = A[left + i - 1]
    for j from 1 to n2: R[j] = A[mid + j]
    i = 1; j = 1; k = left
    while i <= n1 and j <= n2:
        if L[i] <= R[j]:
            A[k] = L[i]; i = i+1
        else:
            A[k] = R[j]; j = j+1
        k = k+1
    while i <= n1:
        A[k] = L[i]; i = i+1; k = k+1
    while j <= n2:
        A[k] = R[j]; j = j+1; k = k+1
```

## Time Complexity
```
T(n) = 2T(n/2) + c.n
Master method: a = 2, b = 2, f(n) = n
n^(log_b a) = n^(log_2 2) = n
f(n) = n = Theta(n^(log_2 2))  =>  Case 2 of master method
T(n) = Theta(n^(log_b a) log n) = Theta(n log n)
```
Space: O(n). Stable.

## Code
```cpp
#include <iostream>
using namespace std;

void merge(int arr[], int left, int mid, int right) {
    int n1 = mid - left + 1;
    int n2 = right - mid;
    int L[n1], R[n2];
    for (int i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (int j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    int i = 0, j = 0, k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j]) {
            arr[k] = L[i];
            i++;
        } else {
            arr[k] = R[j];
            j++;
        }
        k++;
    }
    while (i < n1) {
        arr[k] = L[i];
        i++;
        k++;
    }
    while (j < n2) {
        arr[k] = R[j];
        j++;
        k++;
    }
}

void mergeSort(int arr[], int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        mergeSort(arr, left, mid);
        mergeSort(arr, mid + 1, right);
        merge(arr, left, mid, right);
    }
}

int main() {
    cout<<"Shivansh Kumar\nCSE-C\n12220802723\n";
    int arr[] = {38, 27, 43, 3, 9, 82, 10};
    int n = sizeof(arr) / sizeof(arr[0]);
    mergeSort(arr, 0, n - 1);
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
3 9 10 27 38 43 82
```
