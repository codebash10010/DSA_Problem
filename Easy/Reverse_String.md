# Reverse String - (LeetCode :- 344)

## Difficulty: 🌿 Easy

## 🏢 Companies Asked :- Amazon, Microsoft, Google, Apple

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:  
👉 https://leetcode.com/problems/reverse-string/

---

## 📝 Problem Statement

Write a function that **reverses a string**.

- The input string is given as an **array of characters `s`**.
- You must modify the array **in-place** with **O(1) extra memory**.

---

## 📌 Constraints

- `1 <= s.length <= 10⁵`
- `s[i]` is a **printable ASCII character**.

---

## 📌 Examples

### **Example 1**

**Input:**  
`s = ["h","e","l","l","o"]`

**Output:**  
`["o","l","l","e","h"]`

---

### **Example 2**

**Input:**  
`s = ["H","a","n","n","a","h"]`

**Output:**  
`["h","a","n","n","a","H"]`

---

## 💡 Intuition Behind the Approach

The problem is essentially about **reversing an array of characters in-place**.  
We cannot use extra space, so we must **swap characters directly**.

👉 Key idea:

- Use **two pointers**: one starting at the beginning (`left`) and one at the end (`right`).
- Keep swapping characters at `left` and `right`.
- Move `left++` forward and `right--` backward until they cross.

This ensures the string is reversed **in-place**.

---

## 📚 Algorithm

1. Initialize two pointers:
   - `left = 0`
   - `right = s.length - 1`
2. While `left < right`:
   - Swap `s[left]` and `s[right]`.
   - Move `left++` and `right--`.
3. Done ✅

**Time Complexity:** `O(n)` (one pass).  
**Space Complexity:** `O(1)` (in-place).

---

## 💻 Implementations

### **C++**

```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    void reverseString(vector<char>& s) {
        int left = 0, right = s.size() - 1;
        while (left < right) {
            swap(s[left], s[right]);
            left++;
            right--;
        }
    }
};

// Driver code
int main() {
    int n;
    cout << "Enter size of string: ";
    cin >> n;
    vector<char> s(n);
    cout << "Enter characters: ";
    for (int i = 0; i < n; i++) cin >> s[i];

    Solution sol;
    sol.reverseString(s);

    cout << "Reversed string: ";
    for (char c : s) cout << c << " ";
    cout << endl;
}

```

---

### Java

```java
import java.util.*;

class Solution {
    public void reverseString(char[] s) {
        int left = 0, right = s.length - 1;
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of string: ");
        int n = sc.nextInt();
        char[] s = new char[n];
        System.out.println("Enter characters:");
        for (int i = 0; i < n; i++) {
            s[i] = sc.next().charAt(0);
        }
        Solution sol = new Solution();
        sol.reverseString(s);

        System.out.print("Reversed string: ");
        for (char c : s) System.out.print(c + " ");
    }
}
```

---

### Python

```python
class Solution:
    def reverseString(self, s):
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1

if __name__ == "__main__":
    n = int(input("Enter size of string: "))
    s = list(input("Enter characters without spaces: ")[:n])
    sol = Solution()
    sol.reverseString(s)
    print("Reversed string:", " ".join(s))

```

---

### JavaScript

```javascript
class Solution {
  reverseString(s) {
    let left = 0,
      right = s.length - 1;
    while (left < right) {
      [s[left], s[right]] = [s[right], s[left]];
      left++;
      right--;
    }
  }
}

// Driver
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter size of string: ", (nStr) => {
  readline.question("Enter characters (space-separated): ", (str) => {
    let s = str.trim().split(" ");
    const sol = new Solution();
    sol.reverseString(s);
    console.log("Reversed string:", s.join(" "));
    readline.close();
  });
});
```

---

## 🧪 Tests You Can Try

Input: 28
Output: true

Input: 12
Output: false

Input: 6
Output: true

Input: 496
Output: true

Input: 25
Output: false

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
