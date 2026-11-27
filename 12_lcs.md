# Experiment 12: Longest Common Subsequence (LCS)
**Date:** 10/11/25 | **Page No.:** 25

## Aim
Design and analysis of Longest Common Subsequence.

## Algorithm
Let dp[i][j] = length of LCS of X[0...i-1] and Y[0...j-1]

Recurrence:
```
dp[0][j] = dp[i][0] = 0                       (empty prefix)
if X[i-1] == Y[j-1] then
    dp[i][j] = dp[i-1][j-1] + 1
else
    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

## Complexity
```
T(n) = O(m * n)
```
Space O(m * n).

## Code
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    string a, b;
    cout << "Enter string 1: ";
    cin >> a;
    cout << "Enter string 2: ";
    cin >> b;

    int n = a.size(), m = b.size();
    vector<vector<int>> dp(n+1, vector<int>(m+1, 0));

    for(int i = 1; i <= n; i++){
        for(int j = 1; j <= m; j++){
            if(a[i-1] == b[j-1])
                dp[i][j] = 1 + dp[i-1][j-1];
            else
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
        }
    }

    cout << "LCS length = " << dp[n][m] << endl;
}
```

## Output
```
Enter string 1: ABCDGH
Enter string 2: AEDFHR
LCS length = 3
```
(The LCS is "ADH".)
