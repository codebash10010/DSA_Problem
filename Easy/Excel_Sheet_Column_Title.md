# 168. Excel Sheet Column Title

**Difficulty:** 🟢 Easy  

---

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---
[🔗 Problem Link](https://leetcode.com/problems/excel-sheet-column-title/)

---

## 📝 Problem Statement

Given an integer `columnNumber`, return its corresponding column title as it appears in an Excel sheet.

For example:

```

A -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28
...

````

---

## 📌 Examples

### Example 1
**Input:**  
`columnNumber = 1`  

**Output:**  
`"A"`

---

### Example 2
**Input:**  
`columnNumber = 28`  

**Output:**  
`"AB"`

---

### Example 3
**Input:**  
`columnNumber = 701`  

**Output:**  
`"ZY"`

---

## 💡 Intuition

- This is basically **converting a number into base-26** but with a twist:
  - Excel columns are **1-indexed** (`A=1`, not `0`).
  - After `Z (26)`, it continues with `AA (27)`.

- Trick:
  - Subtract `1` each time (`columnNumber--`) to adjust for **1-indexing**.
  - Take remainder (`% 26`) to get last character.
  - Divide by `26` and repeat.

---

## 📚 Algorithm

1. Initialize an empty result string.
2. While `columnNumber > 0`:
   - Decrement by 1 (`columnNumber--`).
   - Compute remainder = `columnNumber % 26`.
   - Convert to character: `'A' + remainder`.
   - Append to result.
   - Divide `columnNumber //= 26`.
3. Reverse the result string (since we build backwards).

---

## 💻 Implementations (with Driver Code)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string convertToTitle(int columnNumber) {
        string result = "";
        while (columnNumber > 0) {
            columnNumber--;
            int rem = columnNumber % 26;
            result += char('A' + rem);
            columnNumber /= 26;
        }
        reverse(result.begin(), result.end());
        return result;
    }
};

int main() {
    int columnNumber;
    cout << "Enter column number: ";
    cin >> columnNumber;

    Solution sol;
    cout << "Excel Column Title: " << sol.convertToTitle(columnNumber) << endl;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder sb = new StringBuilder();
        while (columnNumber > 0) {
            columnNumber--;
            int rem = columnNumber % 26;
            sb.append((char)('A' + rem));
            columnNumber /= 26;
        }
        return sb.reverse().toString();
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter column number: ");
        int columnNumber = sc.nextInt();

        Solution sol = new Solution();
        System.out.println("Excel Column Title: " + sol.convertToTitle(columnNumber));
    }
}
```

---

### **Python**

```python
class Solution:
    def convertToTitle(self, columnNumber: int) -> str:
        result = []
        while columnNumber > 0:
            columnNumber -= 1
            rem = columnNumber % 26
            result.append(chr(ord('A') + rem))
            columnNumber //= 26
        return ''.join(reversed(result))

if __name__ == "__main__":
    columnNumber = int(input("Enter column number: "))
    sol = Solution()
    print("Excel Column Title:", sol.convertToTitle(columnNumber))
```

---

### **JavaScript (Node.js)**

```javascript
class Solution {
    convertToTitle(columnNumber) {
        let result = "";
        while (columnNumber > 0) {
            columnNumber--;
            let rem = columnNumber % 26;
            result = String.fromCharCode(65 + rem) + result;
            columnNumber = Math.floor(columnNumber / 26);
        }
        return result;
    }
}

// Driver
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question("Enter column number: ", (numStr) => {
    let columnNumber = parseInt(numStr);
    let sol = new Solution();
    console.log("Excel Column Title:", sol.convertToTitle(columnNumber));
    readline.close();
});
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(log₍26₎(n))` → proportional to number of digits in base-26.
* **Space Complexity:** `O(1)` (ignoring output string).

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
