# Experiment 9: N-Queen Problem
**Page No.:** 20-21

## Aim
Design and analysis of N-Queen problem.

## Algorithm
```
NQueens(board, col):
    For each row from 0 to N-1:
        If isSafe(board, row, col) is TRUE then:
            i.   place queen at board[row][col] <- 1
            ii.  If NQueens(board, col+1) = TRUE then
                     return TRUE
            iii. Else
                     board[row][col] <- 0      // Backtrack
    Return FALSE   // No valid position found for this column.

isSafe(board, row, col):
    For i <- 0 to col-1:
        if board[row][i] = 1 then
            return FALSE            // same row attack
    For (i,j) <- (row-1, col-1) to (0,0):
        if board[i][j] = 1 then
            return FALSE            // upper-left diagonal attack
    For (i,j) <- (row+1, col-1) to (N-1, 0):
        if board[i][j] = 1 then
            return FALSE            // lower-left diagonal attack
    RETURN TRUE
```

## Time Complexity
```
T(n) = O(N!)
```

## Code
```cpp
#include <iostream>
#include <vector>
using namespace std;

bool isSafe(const vector<vector<int>>& board, int row, int col, int n) {
    for (int i = 0; i < row; i++)
        if (board[i][col])
            return false;
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
        if (board[i][j])
            return false;
    for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
        if (board[i][j])
            return false;
    return true;
}

bool solveNQueen(vector<vector<int>>& board, int row, int n) {
    if (row == n)
        return true;
    for (int col = 0; col < n; col++) {
        if (isSafe(board, row, col, n)) {
            board[row][col] = 1;
            if (solveNQueen(board, row + 1, n))
                return true;
            board[row][col] = 0;
        }
    }
    return false;
}

int main() {
    int n;
    cout << "Enter the number of queens: ";
    cin >> n;
    vector<vector<int>> board(n, vector<int>(n, 0));
    if (solveNQueen(board, 0, n)) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++)
                cout << (board[i][j] ? "Q " : ". ");
            cout << endl;
        }
    } else {
        cout << "No solution exists." << endl;
    }
    return 0;
}
```

## Output
```
Enter the number of queens: 8
Q . . . . . . .
. . . . Q . . .
. . . . . . . Q
. . . . . Q . .
. . Q . . . . .
. . . . . . Q .
. Q . . . . . .
. . . Q . . . .
```
