
# 392. Is Subsequence

**Difficulty:** 🟢 Easy  

---

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

[🔗 Problem Link](https://leetcode.com/problems/is-subsequence/) :contentReference[oaicite:0]{index=0}

---

## 📝 Problem Statement

You are given two strings `s` and `t`. Return `true` *if* `s` is a **subsequence** of `t`, and `false` otherwise.

A **subsequence** of a string is a new string formed from the original string by deleting some (can be none) of the characters **without changing the order** of the remaining characters.

- For example:
  - `"ace"` is a subsequence of `"abcde"` (delete `b` and `d`).
  - `"aec"` is *not* a subsequence of `"abcde"` (order is broken).

---

## 📌 Constraints

- `0 <= s.length <= 100`
- `0 <= t.length <= 10⁴` :contentReference[oaicite:1]{index=1}  
- `s` and `t` consist only of lowercase English letters. :contentReference[oaicite:2]{index=2}

---

## ✅ Examples

| Example | Input | Output | Explanation |
|--------|--------|--------|-------------|
| 1 | `s = "abc"`, `t = "ahbgdc"` | `true` | We can pick `a`, then `b`, then `c` in order from `t`. |
| 2 | `s = "axc"`, `t = "ahbgdc"` | `false` | `x` cannot be matched in the correct order. |

---

## 💡 Intuition & Approach

To check whether `s` is a subsequence of `t`, we want to see if we can “walk through” `t` and pick characters that match `s` in order.

A natural approach: **two pointers**:

- One pointer `i` scans through `s` (the target subsequence we want).
- Another pointer `j` scans through `t` (the longer string).
- As we walk through `t`, whenever `t[j]` matches `s[i]`, we advance `i` (we found that character).
- Regardless of match or not, we always advance `j`.
- If at the end `i == len(s)`, we matched all of `s` → return `true`.

This is greedy and optimal, and it runs in **O(|t| + |s|)** time (effectively O(|t|) since |s| ≤ |t|). It uses only a few pointers → **O(1)** extra space.

---

## 📚 Algorithm Steps

1. Initialize `i = 0` (for `s`), `j = 0` (for `t`).
2. While `i < len(s)` **and** `j < len(t)`:
   - If `s[i] == t[j]`, increment `i`.
   - Always increment `j`.
3. After loop, check: if `i == len(s)`, return `true`, else `false`.

Edge cases:
- If `s` is empty → automatically `true`.
- If `t` is empty but `s` is nonempty → `false`.

---

## 💻 Implementations (with Driver Code for User Input)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    bool isSubsequence(string s, string t) {
        int i = 0, j = 0;
        int n = s.size(), m = t.size();
        while (i < n && j < m) {
            if (s[i] == t[j]) {
                i++;
            }
            j++;
        }
        return (i == n);
    }
};

int main() {
    string s, t;
    cout << "Enter s (subsequence string): ";
    cin >> s;
    cout << "Enter t (target string): ";
    cin >> t;

    Solution sol;
    bool ans = sol.isSubsequence(s, t);
    cout << (ans ? "true" : "false") << endl;
    return 0;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public boolean isSubsequence(String s, String t) {
        int i = 0, j = 0;
        int n = s.length(), m = t.length();
        while (i < n && j < m) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
            }
            j++;
        }
        return (i == n);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter s (subsequence string): ");
        String s = sc.next();
        System.out.print("Enter t (target string): ");
        String t = sc.next();

        Solution sol = new Solution();
        boolean ans = sol.isSubsequence(s, t);
        System.out.println(ans);
    }
}
```

---

### **Python**

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i, j = 0, 0
        n, m = len(s), len(t)
        while i < n and j < m:
            if s[i] == t[j]:
                i += 1
            j += 1
        return i == n

if __name__ == "__main__":
    s = input("Enter s (subsequence string): ").strip()
    t = input("Enter t (target string): ").strip()
    sol = Solution()
    print(sol.isSubsequence(s, t))
```

---

### **JavaScript (Node.js)**

```javascript
class Solution {
    isSubsequence(s, t) {
        let i = 0, j = 0;
        const n = s.length, m = t.length;
        while (i < n && j < m) {
            if (s[i] === t[j]) {
                i++;
            }
            j++;
        }
        return i === n;
    }
}

// Driver for user input
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout
});

readline.question("Enter s (subsequence string): ", (s) => {
    readline.question("Enter t (target string): ", (t) => {
        const sol = new Solution();
        const ans = sol.isSubsequence(s, t);
        console.log(ans);
        readline.close();
    });
});
```

---

## ⏱️ Time & Space Complexity

* **Time Complexity:** `O(n + m)` where `n = |s|` and `m = |t|`. In the worst case, we scan all of `t`.
* **Space Complexity:** `O(1)` — only constant extra space is used (a couple of pointers).

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

### **JavaScript (Node.js)**

```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---