# Experiment 5: Strassen's Matrix Multiplication
**Date:** 25/8/25 | **Page No.:** 12-13

## Aim
Design and analysis of Strassen's matrix multiplication algorithm.

## Algorithm
```
StrassenMultiply(A, B, n):
    if n == 1:
        C[0][0] = A[0][0] * B[0][0]
        return C
    k = n/2
    A = [A11 A12; A21 A22]     B = [B11 B12; B21 B22]

    M1 = StrassenMultiply(A11 + A22, B11 + B22, k)
    M2 = StrassenMultiply(A21 + A22, B11, k)
    M3 = StrassenMultiply(A11, B12 - B22, k)
    M4 = StrassenMultiply(A22, B21 - B11, k)
    M5 = StrassenMultiply(A11 + A12, B22, k)
    M6 = StrassenMultiply(A21 - A11, B11 + B12, k)
    M7 = StrassenMultiply(A12 - A22, B21 + B22, k)

    C11 = M1 + M4 - M5 + M7
    C12 = M3 + M5
    C21 = M2 + M4
    C22 = M1 - M2 + M3 + M6

    for i from 0 to k-1:
        for j from 0 to k-1:
            C[i][j]     = C11[i][j]
            C[i][j+k]   = C12[i][j]
            C[i+k][j]   = C21[i][j]
            C[i+k][j+k] = C22[i][j]
    return C
```

## Time Complexity
```
T(n) = Theta(1)              n < 2
     = 7T(n/2) + Theta(n^2)  otherwise

Master method: a = 7, b = 2, n^(log_b a) = n^(log_2 7) = n^2.81,  f(n) = n^2
f(n) = n^2 = O(n^(log_2 7 - e))  =>  Case 1 of master method
T(n) = Theta(n^(log_2 7)) = O(n^2.81)
```

## Code
```cpp
#include <iostream>
#include <vector>
using namespace std;
typedef vector<vector<int>> Matrix;

Matrix add(const Matrix &A, const Matrix &B) {
    int n = A.size();
    Matrix C(n, vector<int>(n));
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            C[i][j] = A[i][j] + B[i][j];
    return C;
}
Matrix subtract(const Matrix &A, const Matrix &B) {
    int n = A.size();
    Matrix C(n, vector<int>(n));
    for (int i = 0; i < n; i++)
        for (int j = 0; j < n; j++)
            C[i][j] = A[i][j] - B[i][j];
    return C;
}
Matrix strassen(const Matrix &A, const Matrix &B) {
    int n = A.size();
    if (n == 1) {
        Matrix C(1, vector<int>(1));
        C[0][0] = A[0][0] * B[0][0];
        return C;
    }
    int k = n / 2;
    Matrix A11(k, vector<int>(k)), A12(k, vector<int>(k)), A21(k, vector<int>(k)), A22(k, vector<int>(k));
    Matrix B11(k, vector<int>(k)), B12(k, vector<int>(k)), B21(k, vector<int>(k)), B22(k, vector<int>(k));

    for (int i = 0; i < k; i++)
        for (int j = 0; j < k; j++) {
            A11[i][j] = A[i][j];
            A12[i][j] = A[i][j + k];
            A21[i][j] = A[i + k][j];
            A22[i][j] = A[i + k][j + k];
            B11[i][j] = B[i][j];
            B12[i][j] = B[i][j + k];
            B21[i][j] = B[i + k][j];
            B22[i][j] = B[i + k][j + k];
        }
    Matrix M1 = strassen(add(A11, A22), add(B11, B22));
    Matrix M2 = strassen(add(A21, A22), B11);
    Matrix M3 = strassen(A11, subtract(B12, B22));
    Matrix M4 = strassen(A22, subtract(B21, B11));
    Matrix M5 = strassen(add(A11, A12), B22);
    Matrix M6 = strassen(subtract(A21, A11), add(B11, B12));
    Matrix M7 = strassen(subtract(A12, A22), add(B21, B22));
    Matrix C11 = add(subtract(add(M1, M4), M5), M7);
    Matrix C12 = add(M3, M5);
    Matrix C21 = add(M2, M4);
    Matrix C22 = add(subtract(add(M1, M3), M2), M6);
    Matrix C(n, vector<int>(n));
    for (int i = 0; i < k; i++)
        for (int j = 0; j < k; j++) {
            C[i][j] = C11[i][j];
            C[i][j + k] = C12[i][j];
            C[i + k][j] = C21[i][j];
            C[i + k][j + k] = C22[i][j];
        }
    return C;
}
int main() {
    cout<<"Shivansh Kumar\nCSE-C\n12220802723\n\n";
    int n = 4;
    Matrix A = {{1, 2, 3, 4}, {5, 6, 7, 8}, {9, 10, 11, 12}, {13, 14, 15, 16}};
    Matrix B = {{17, 18, 19, 20}, {21, 22, 23, 24}, {25, 26, 27, 28}, {29, 30, 31, 32}};
    Matrix C = strassen(A, B);
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++)
            cout << C[i][j] << " ";
        cout << endl;
    }
    return 0;
}
```
> Works only when n is a power of 2.

## Output
```
Shivansh Kumar
CSE-C
12220802723

250 260 270 280
618 644 670 696
986 1028 1070 1112
1354 1412 1470 1528
```
