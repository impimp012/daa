# Experiment 11: String Matching - KMP Algorithm
**Date:** 10/11/25 | **Page No.:** 23-24

## Aim
Design and analysis of string matching KMP algorithm.

## Algorithm
```
void computeLPS(P, lps):
    int m = P.length();
    int len = 0
    lps[0] = 0
    int i = 1;
    while (i < m) {
        if (P[i] == P[len]) {
            len++;
            lps[i] = len;
            i++;
        } else {
            if (len != 0) {
                len = lps[len-1];
            } else {
                lps[i] = 0; i++;
            }
        }
    }

void KMPSearch(string T, string P) {
    int n = T.length();
    int m = P.length();
    computeLPS(P, lps)
    int i = 0;
    int j = 0;
    while (i < n) {
        if (T[i] == P[j]) {
            i++;
            j++;
        }
        if (j == m) {
            pattern found;
            j = lps[j-1];
        } else if (i < n && T[i] != P[j]) {
            if (j != 0)
                j = lps[j-1];
            else
                i++;
        }
    }
}
```

## Time Complexity
```
prefix function    => O(m)
pattern searching  => O(n)
T(n) = O(n + m)
```

## Code
```cpp
#include <bits/stdc++.h>
using namespace std;

// Build LPS (Longest Prefix Suffix) array
vector<int> buildLPS(string p) {
    int n = p.size(), j = 0;
    vector<int> lps(n, 0);
    for (int i = 1; i < n; i++) {
        while (j > 0 && p[i] != p[j]) j = lps[j - 1];
        if (p[i] == p[j]) j++;
        lps[i] = j;
    }
    return lps;
}

// KMP Search
void KMP(string t, string p) {
    vector<int> lps = buildLPS(p);
    int i = 0, j = 0;

    while (i < t.size()) {
        if (t[i] == p[j]) { i++; j++; }

        if (j == p.size()) {
            cout << "Pattern found at index " << i - j << "\n";
            j = lps[j - 1];  // continue searching
        }
        else if (i < t.size() && t[i] != p[j]) {
            if (j != 0) j = lps[j - 1];
            else i++;
        }
    }
}

int main() {
    string t, p;
    cout << "Enter text: ";
    cin >> t;
    cout << "Enter pattern: ";
    cin >> p;

    KMP(t, p);
}
```

## Output
```
Enter text: ababcabcabababd
Enter pattern: ababd
Pattern found at index 10
```
