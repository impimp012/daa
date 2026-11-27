# Experiment 7: Huffman Coding
**Date:** 8/9/25 | **Page No.:** 16-17

## Aim
Design and analysis of Huffman coding algorithm.

## Algorithm
```
HuffmanCoding(text):
    If text is empty Then Return
    freq_map = count frequencies in text              -> O(N)
    pq = min-heap of (char, freq) nodes from freq_map -> O(log n) per insert
    WHILE pq.size() > 1 DO
        left  = pq.pop()
        right = pq.pop()
        merged = Node('$', left.freq + right.freq)
        merged.left  = left
        merged.right = right
        pq.push(merged)                               -> O(n log n)
    root = pq.top()
    codes_map = empty map
    GenerateCodes(root, "", codes_map)
    encoded_string = concatenate codes_map[ch] for each ch in text
    Print codes_map and encoded_string

function GenerateCodes(node, code, codes_map):        -> O(n)
    If node is NULL then Return
    If node is leaf then
        codes_map[node.ch] = code
    Else
        GenerateCodes(node.left,  code + "0", codes_map)
        GenerateCodes(node.right, code + "1", codes_map)
```

## Time Complexity
```
T(n) = O(n log n)
```
(n = number of distinct characters.) Space O(n).

## Code
```cpp
#include <bits/stdc++.h>
using namespace std;
struct Node {
    char ch;
    int freq;
    Node *left, *right;
    Node(char c, int f) : ch(c), freq(f), left(nullptr), right(nullptr) {}
};
struct Compare {
    bool operator()(Node* l, Node* r) {
        return l->freq > r->freq;
    }
};
void generateCodes(Node* root, string str, unordered_map<char, string>& codes) {
    if (!root) return;
    if (!root->left && !root->right) {
        codes[root->ch] = str;
    }
    generateCodes(root->left, str + "0", codes);
    generateCodes(root->right, str + "1", codes);
}
void huffmanCoding(const string& text) {
    if (text.empty()) {
        cout << "Input text is empty!\n";
        return;
    }
    unordered_map<char, int> freq;
    for (char ch : text) freq[ch]++;

    priority_queue<Node*, vector<Node*>, Compare> pq;
    for (auto& pair : freq) pq.push(new Node(pair.first, pair.second));

    while (pq.size() > 1) {
        Node* left = pq.top(); pq.pop();
        Node* right = pq.top(); pq.pop();
        Node* newNode = new Node('$', left->freq + right->freq);
        newNode->left = left;
        newNode->right = right;
        pq.push(newNode);
    }
    Node* root = pq.top();
    unordered_map<char, string> codes;
    generateCodes(root, "", codes);

    cout << "\nCharacter Codes:\n";
    for (auto& pair : codes) {
        cout << pair.first << ": " << pair.second << "\n";
    }

    string encodedStr = "";
    for (char ch : text) encodedStr += codes[ch];

    cout << "\nEncoded string:\n" << encodedStr << "\n";
}
int main() {
    cout << "Shivansh Kumar  CSE-C\n12220802723\n";
    string text;
    cout << "Enter the text: ";
    getline(cin, text);
    huffmanCoding(text);
    return 0;
}
```
> The first `cout` line (name/roll number) is not visible in the printed code of your file but appears in your output, so it is included here.

## Output
```
Shivansh Kumar  CSE-C
12220802723
Enter the text: WORLD

Character Codes:
L: 00
W: 01
R: 110
O: 111
D: 10

Encoded string:
011111100010
```
