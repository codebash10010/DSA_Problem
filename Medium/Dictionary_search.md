# Design Add and Search Words Data Structure - (LeetCode :- 211)

## 🏢 Companies Asked :- Google✯, Amazon✯, Microsoft✯, Meta✯, Bloomberg✯, Apple✯, Adobe, Oracle, Uber, Spotify

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/design-add-and-search-words-data-structure/description/)

---

## 🧩 Problem Statement

Design a data structure that supports adding new words and finding if a string matches any previously added word.

Implement the `WordDictionary` class:

* `WordDictionary()` → Initializes the object.
* `void addWord(word)` → Adds a word into the data structure.
* `bool search(word)` → Returns true if there is any string that matches the word (including `.` wildcards).

`.` can represent any single letter.

---

### Example

**Input:**

```
["WordDictionary", "addWord", "addWord", "addWord", "search", "search", "search", "search"]
[[], ["bad"], ["dad"], ["mad"], ["pad"], ["bad"], [".ad"], ["b.."]]
```

**Output:**

```
[null, null, null, null, false, true, true, true]
```

**Explanation:**

```
WordDictionary wordDictionary = new WordDictionary();
wordDictionary.addWord("bad");
wordDictionary.addWord("dad");
wordDictionary.addWord("mad");
wordDictionary.search("pad"); // false
wordDictionary.search("bad"); // true
wordDictionary.search(".ad"); // true
wordDictionary.search("b.."); // true
```

---

## 💡 Intuition

We need to store many words and support flexible search queries (with `.` wildcards).
A **Trie (Prefix Tree)** is perfect for this because:

* It allows **fast prefix lookups**.
* The wildcard `.` can be handled using **Depth-First Search (DFS)** across all possible children.

✅ `addWord()` → builds the Trie.
✅ `search()` → explores all valid paths recursively when encountering `.`.

---

## ⚙️ Approach

1. Create a **TrieNode** class with:

   * `children[26]` for lowercase letters.
   * `isEnd` flag to mark the end of a word.
2. For **addWord(word)**:

   * Traverse or create new nodes for each character.
3. For **search(word)**:

   * Use recursion (DFS):

     * If current char is `.`, try all possible children.
     * Otherwise, follow the path for that letter.
4. Return true if a valid word ends at the final node.

---

## 🧠 Example Dry Run

**Added words:** `bad`, `dad`, `mad`
**Search:** `"b.."`

```
'b' -> exists
'.' -> try all children: 'a', etc.
'.' -> try all children again
End of word -> return true
```

✅ Output → `true`

---

## 🧩 Code Implementations

---

### 🧱 C++ Solution (with User Input)

```cpp
#include <bits/stdc++.h>
using namespace std;

class TrieNode {
public:
    TrieNode* children[26];
    bool isEnd;
    TrieNode() {
        isEnd = false;
        for (int i = 0; i < 26; i++) children[i] = nullptr;
    }
};

class WordDictionary {
    TrieNode* root;
    bool dfs(string& word, int i, TrieNode* node) {
        if (i == word.size()) return node->isEnd;
        char c = word[i];
        if (c == '.') {
            for (int j = 0; j < 26; j++)
                if (node->children[j] && dfs(word, i + 1, node->children[j]))
                    return true;
            return false;
        } else {
            if (!node->children[c - 'a']) return false;
            return dfs(word, i + 1, node->children[c - 'a']);
        }
    }

public:
    WordDictionary() { root = new TrieNode(); }

    void addWord(string word) {
        TrieNode* node = root;
        for (char c : word) {
            if (!node->children[c - 'a'])
                node->children[c - 'a'] = new TrieNode();
            node = node->children[c - 'a'];
        }
        node->isEnd = true;
    }

    bool search(string word) { return dfs(word, 0, root); }
};

int main() {
    WordDictionary dict;
    int n;
    cout << "Enter number of operations: ";
    cin >> n;

    while (n--) {
        string op, word;
        cin >> op >> word;
        if (op == "add")
            dict.addWord(word);
        else if (op == "search")
            cout << (dict.search(word) ? "true" : "false") << endl;
    }
}
```

---

### ☕ Java Solution (with User Input)

```java
import java.util.*;

class TrieNode {
    TrieNode[] children = new TrieNode[26];
    boolean isEnd = false;
}

class WordDictionary {
    private TrieNode root = new TrieNode();

    public void addWord(String word) {
        TrieNode node = root;
        for (char c : word.toCharArray()) {
            if (node.children[c - 'a'] == null)
                node.children[c - 'a'] = new TrieNode();
            node = node.children[c - 'a'];
        }
        node.isEnd = true;
    }

    public boolean search(String word) {
        return dfs(word, 0, root);
    }

    private boolean dfs(String word, int i, TrieNode node) {
        if (i == word.length()) return node.isEnd;
        char c = word.charAt(i);
        if (c == '.') {
            for (TrieNode child : node.children)
                if (child != null && dfs(word, i + 1, child))
                    return true;
            return false;
        } else {
            if (node.children[c - 'a'] == null) return false;
            return dfs(word, i + 1, node.children[c - 'a']);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        WordDictionary dict = new WordDictionary();
        int n = sc.nextInt();

        for (int i = 0; i < n; i++) {
            String op = sc.next();
            String word = sc.next();
            if (op.equals("add")) dict.addWord(word);
            else if (op.equals("search"))
                System.out.println(dict.search(word));
        }
    }
}
```

---

### 🐍 Python Solution (with User Input)

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.isEnd = False

class WordDictionary:
    def __init__(self):
        self.root = TrieNode()

    def addWord(self, word):
        node = self.root
        for c in word:
            if c not in node.children:
                node.children[c] = TrieNode()
            node = node.children[c]
        node.isEnd = True

    def search(self, word):
        def dfs(node, i):
            if i == len(word): return node.isEnd
            if word[i] == '.':
                for child in node.children.values():
                    if dfs(child, i + 1): return True
                return False
            if word[i] not in node.children:
                return False
            return dfs(node.children[word[i]], i + 1)
        return dfs(self.root, 0)

if __name__ == "__main__":
    wd = WordDictionary()
    n = int(input("Enter number of operations: "))
    for _ in range(n):
        op, word = input().split()
        if op == "add":
            wd.addWord(word)
        else:
            print(wd.search(word))
```

---

### ⚡ JavaScript Solution (with User Input)

```javascript
class TrieNode {
  constructor() {
    this.children = {};
    this.isEnd = false;
  }
}

class WordDictionary {
  constructor() {
    this.root = new TrieNode();
  }

  addWord(word) {
    let node = this.root;
    for (let c of word) {
      if (!node.children[c]) node.children[c] = new TrieNode();
      node = node.children[c];
    }
    node.isEnd = true;
  }

  search(word) {
    const dfs = (node, i) => {
      if (i === word.length) return node.isEnd;
      if (word[i] === ".") {
        for (let key in node.children)
          if (dfs(node.children[key], i + 1)) return true;
        return false;
      }
      if (!node.children[word[i]]) return false;
      return dfs(node.children[word[i]], i + 1);
    };
    return dfs(this.root, 0);
  }
}

const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter number of operations: ", (n) => {
  const dict = new WordDictionary();
  let count = 0;

  const getInput = () => {
    if (count === parseInt(n)) {
      readline.close();
      return;
    }
    readline.question("", (line) => {
      const [op, word] = line.split(" ");
      if (op === "add") dict.addWord(word);
      else console.log(dict.search(word));
      count++;
      getInput();
    });
  };
  getInput();
});
```

---

## 🧪 Sample Run

**Input**

```
7
add bad
add dad
add mad
search pad
search bad
search .ad
search b..
```

**Output**

```
false
true
true
true
```

---

## 🕒 Complexity

| Operation | Time            | Space    |
| --------- | --------------- | -------- |
| `addWord` | O(L)            | O(L × N) |
| `search`  | O(L × 26) worst | O(L)     |

Where `L` is the average word length, and `N` is the number of words.

---

## 🚀 How to Run

### **C++**

```bash
g++ solution.cpp -o solution
./solution
```

### **Java**

```bash
javac Main.java
java Main
```

### **Python**

```bash
python solution.py
```

### **JavaScript**

```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---
