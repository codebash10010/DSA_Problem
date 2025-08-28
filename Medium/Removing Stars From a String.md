# 2390. Removing Stars From a String

**Difficulty:** Medium

## 🏢 Companies Asked :- Amazon

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## Problem

You are given a string `s`, which contains stars `*`.

In one operation, you can:

- Choose a star in `s`.
- Remove the closest non-star character to its left, as well as remove the star itself.

Return the string after all stars have been removed.

**Note:**

- The input will be generated such that the operation is always possible.
- It can be shown that the resulting string will always be unique.

---

## Examples

**Example 1:**

```
Input: s = "leet**cod*e"
Output: "lecoe"
```

**Explanation:** Performing the removals from left to right:

- The closest character to the 1st star is 't' in "leet\*\*cod*e". `s` becomes "lee*cod\*e".
- The closest character to the 2nd star is 'e' in "lee*cod*e". `s` becomes "lecod\*e".
- The closest character to the 3rd star is 'd' in "lecod\*e". `s` becomes "lecoe".

**Example 2:**

```
Input: s = "erase*****"
Output: ""
```

---

## Constraints

- `1 <= s.length <= 10^5`
- `s` consists of lowercase English letters and stars `*`.
- The operation above can be performed on `s`.

---

## Intuition

Each `*` removes the closest previous non-star character and itself. This behavior maps naturally to using a stack (or a dynamic result buffer):

- Iterate characters from left to right.
- If character is a lowercase letter, push it onto the stack (or append to result buffer).
- If character is `*`, pop the last letter from the stack (or remove last character from result buffer).

Because the input guarantees every star has a character to remove, you don't need extra checks beyond safe pops when implemented correctly.

This yields an O(n) time algorithm and O(n) worst-case extra space for the stack / buffer.

---

## Approach

1. Initialize an empty list `res` (acts like a stack).
2. For each character `ch` in `s`:

   - If `ch` is not `*`, append `ch` to `res`.
   - Else (it's `*`), pop the last element from `res` (remove last character).

3. Join the list `res` into a string and return.

---

## Complexity

- **Time:** O(n), where n = length of `s`. We process each character once.
- **Space:** O(n) worst-case for the stack / result buffer.

---

## Edge cases

- The result can be an empty string (e.g., all characters removed).
- Many consecutive stars are handled naturally by repeated pops.
- Large `s` (up to `10^5`) is fine with the O(n) algorithm.

---

## Implementations

### C++

### **C++**

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


int main() {
string s;
cin >> s;
Solution sol;
cout << sol.removeStars(s) << "\n";
return 0;
}
```

### Java
---
```java
import java.util.*;


class Solution {
public String removeStars(String s) {
StringBuilder sb = new StringBuilder();
for (char c : s.toCharArray()) {
if (c == '*') {
sb.deleteCharAt(sb.length()-1);
} else {
sb.append(c);
}
}
return sb.toString();
}


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


if __name__ == "__main__":
s = input().strip()
sol = Solution()
print(sol.removeStars(s))
```
---
### JavaScript

```JavaScript

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
## Tests you can try

* `"leet**cod*e"` -> `"lecoe"`
* `"erase*****"` -> `""`
* `"a*b*c*"` -> `""` (interleaved removals)
* `"abc"` -> `"abc"` (no stars)

---

## Notes

* The stack approach is straightforward and optimal for this problem.
* If memory must be minimized and input is streaming, the same logic applies using an output buffer and tracking its length.

---

**Tags:** string, stack, simulation, two-pointers (conceptual)

---

## 🚀 How to Run

### **C++**
```bash
g++ solution.cpp -o solution
./solution
````

### **Java**

```bash
javac Solution.java
java Solution
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
