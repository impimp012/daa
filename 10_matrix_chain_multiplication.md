# Experiment 10: Matrix Chain Multiplication
**Date:** 3/11/25 | **Page No.:** 22

## Aim
Design and analysis of Matrix Chain Multiplication.

## Algorithm
```
MatrixChainOrder(p):
    n = len(p) - 1
    let m[1..n][1..n] and s[1..n][1..n]
    for i = 1 to n:
        m[i][i] = 0
    for L = 2 to n:
        for i = 1 to n-L+1:
            j = i + L - 1
            m[i][j] = +infinity
            for k = i to j-1:
                q = m[i][k] + m[k+1][j] + p[i-1] * p[k] * p[j]
                if q < m[i][j]:
                    m[i][j] = q
                    s[i][j] = k
    return m, s
```

## Time Complexity
```
T(n) = O(n^3)
```
Space O(n^2).

## Code
```cpp
#include <iostream>
#include <vector>
#include <climits>
using namespace std;

// Function to print the optimal parenthesization
void printParenthesis(int i, int j, int n, vector<vector<int>> &bracket, char &name) {
    if (i == j) {
        cout << name++;
        return;
    }

    cout << "(";
    printParenthesis(i, bracket[i][j], n, bracket, name);
    printParenthesis(bracket[i][j] + 1, j, n, bracket, name);
    cout << ")";
}

// Matrix Chain Multiplication function
void matrixChainOrder(vector<int> p, int n) {
    // m[i][j] = Minimum number of multiplications needed to multiply matrices from i to j
    vector<vector<int>> m(n, vector<int>(n, 0));
    // bracket[i][j] = index at which the product is split to get optimal cost
    vector<vector<int>> bracket(n, vector<int>(n, 0));

    // L is chain length
    for (int L = 2; L < n; L++) {
        for (int i = 1; i < n - L + 1; i++) {
            int j = i + L - 1;
            m[i][j] = INT_MAX;
            for (int k = i; k < j; k++) {
                int q = m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j];
                if (q < m[i][j]) {
                    m[i][j] = q;
                    bracket[i][j] = k;
                }
            }
        }
    }
    cout << "Minimum number of multiplications: " << m[1][n - 1] << endl;
    cout << "Optimal Parenthesization: ";
    char name = 'A';
    printParenthesis(1, n - 1, n, bracket, name);
    cout << endl;
}

int main() {
    int n;
    cout << "Enter number of matrices: ";
    cin >> n;
    vector<int> p(n + 1);
    cout << "Enter dimensions (e.g., for matrices A1: 10x20, A2: 20x30 -> enter 10 20 30): ";
    for (int i = 0; i <= n; i++) {
        cin >> p[i];
    }

    matrixChainOrder(p, n + 1);
    return 0;
}
```

## Output
```
Enter number of matrices: 3
Enter dimensions (e.g., for matrices A1: 10x20, A2: 20x30 -> enter 10 20 30): 10 20 30 50
Minimum number of multiplications: 21000
Optimal Parenthesization: ((AB)C)
```
Check: (AB)C = 10*20*30 + 10*30*50 = 6000 + 15000 = 21000.
