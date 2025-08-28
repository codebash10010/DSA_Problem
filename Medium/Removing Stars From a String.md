# 2390. Removing Stars From a String

**Difficulty:** Medium

**🏢 Companies Asked:** Amazon

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## Problem

You are given a string `s`, which contains stars `*`.

In one operation, you can:

* Choose a star in `s`.
* Remove the closest non-star character to its left, as well as remove the star itself.

Return the string after all stars have been removed.

**Note:**

* The input will be generated such that the operation is always possible.
* It can be shown that the resulting string will always be unique.

---

## Examples

**Example 1:**

```text
Input: s = "leet**cod*e"
Output: "lecoe"
```

**Explanation:**

* The closest character to the 1st star is 't' in `leet**cod*e` → `lee*cod*e`.
* The closest character to the 2nd star is 'e' in `lee*cod*e` → `lecod*e`.
* The closest character to the 3rd star is 'd' in `lecod*e` → `lecoe`.

**Example 2:**

```text
Input: s = "erase*****"
Output: ""
```

---

## Constraints

* `1 <= s.length <= 10^5`
* `s` consists of lowercase English letters and stars `*`.
* The operation above can be performed on `s`.

---

## Intuition

Each `*` removes the closest previous non-star character and itself. This maps naturally to a **stack-like approach**:

* Traverse string left → right.
* If character is a letter → push it to stack.
* If character is `*` → pop from stack.

---

## Approach

1. Initialize an empty list `res`.
2. Traverse string:

   * If char is letter → append to `res`.
   * If char is `*` → pop last element from `res`.
3. Return the joined string from `res`.

---

## Complexity

* **Time:** O(n)
* **Space:** O(n) (worst case stack size)

---

## Edge Cases

* Entire string becomes empty.
* Consecutive stars work naturally.
* Large input (`10^5` length).

---

## Implementations

### C++

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string removeStars(string s) {
        string res;
        res.reserve(s.size());
        for (char c : s) {
            if (c == '*') {
                if (!res.empty()) res.pop_back();
            } else {
                res.push_back(c);
            }
        }
        return res;
    }
};
// Driver code
int main() {
    string s;
    cin >> s;
    Solution sol;
    cout << sol.removeStars(s) << "\n";
    return 0;
}
```

---

### Java

```java
import java.util.*;

class Solution {
    public String removeStars(String s) {
        StringBuilder sb = new StringBuilder();
        for (char c : s.toCharArray()) {
            if (c == '*') {
                sb.deleteCharAt(sb.length() - 1);
            } else {
                sb.append(c);
            }
        }
        return sb.toString();
    }
// Driver code
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        Solution sol = new Solution();
        System.out.println(sol.removeStars(s));
    }
}
```

---

### Python

```python
class Solution:
    def removeStars(self, s: str) -> str:
        res = []
        for ch in s:
            if ch == '*':
                res.pop()
            else:
                res.append(ch)
        return ''.join(res)
# Driver code
if __name__ == "__main__":
    s = input().strip()
    sol = Solution()
    print(sol.removeStars(s))
```

---

### JavaScript (Node.js)

```javascript
function removeStars(s) {
  const res = [];
  for (const ch of s) {
    if (ch === '*') {
      res.pop();
    } else {
      res.push(ch);
    }
  }
  return res.join('');
}

// Driver code
const readline = require("readline");
const rl = readline.createInterface({ input: process.stdin, output: process.stdout });

rl.question("", function(s) {
  console.log(removeStars(s.trim()));
  rl.close();
});
```

---

## 🧪 Tests You Can Try

* `leet**cod*e` → `lecoe`
* `erase*****` → \`\` (empty)
* `a*b*c*` → \`\` (empty)
* `abc` → `abc` (no stars)

---

## 🚀 How to Run

### **C++**

```bash
g++ solution.cpp -o solution
./solution
```

### **Java**

```bash
javac Solution.java
java Solution
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
