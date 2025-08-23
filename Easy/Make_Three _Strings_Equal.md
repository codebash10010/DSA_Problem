# Make Three Strings Equal - (LeetCode :- 2937)

## 🏢 Companies Asked :- Amazon, Google, Microsoft  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/make-three-strings-equal/

---

## 📝 Problem Statement

You are given three strings: `s1`, `s2`, and `s3`.  

In **one operation**, you can choose one of these strings and delete its **rightmost character**.  
⚠️ You cannot completely empty a string.  

Return the **minimum number of operations** required to make the strings equal.  
If it is **impossible** to make them equal, return `-1`.

---

## 📌 Constraints
- `1 <= s1.length, s2.length, s3.length <= 100`  
- `s1`, `s2`, and `s3` consist only of **lowercase English letters**

---

## 📌 Examples

### **Example 1**
**Input:**  
s1 = "abc", s2 = "abb", s3 = "ab"


**Output:**  

2


**Explanation:**  
- Delete last character from `s1 → "ab"`  
- Delete last character from `s2 → "ab"`  
Now all strings are `"ab"` → 2 operations ✅  

---

### **Example 2**
**Input:**  


s1 = "dac", s2 = "bac", s3 = "cac"

**Output:**  

-1

**Explanation:**  
- Since the first letters differ (`d`, `b`, `c`) → it’s **impossible** to make them equal by only removing suffixes.  

---

## 💡 Intuition Behind the Approach

The only valid operation is **removing characters from the end**.  
So the only possible common string must be a **common prefix** of all three strings.  

👉 Therefore:  
1. Find the **longest common prefix** among `s1`, `s2`, and `s3`.  
2. Let its length = `L`.  
3. The answer = `(len(s1) - L) + (len(s2) - L) + (len(s3) - L)`  
   - i.e., total characters to delete beyond the common prefix.  

⚠️ If there’s **no common prefix**, return `-1`.  

---

## 📚 Algorithm Explanation

1. Start comparing characters from the **first index** across all three strings.  
2. Stop when characters differ or any string ends.  
3. Let `L = length of common prefix`.  
   - If `L == 0`, return `-1`.  
   - Otherwise, result = `(len(s1) - L) + (len(s2) - L) + (len(s3) - L)`.  

**Time Complexity:** `O(min(n1, n2, n3))`  
**Space Complexity:** `O(1)`  

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <string>
using namespace std;

class Solution {
public:
    int findMinimumOperations(string s1, string s2, string s3) {
        int n1 = s1.size(), n2 = s2.size(), n3 = s3.size();
        int L = 0;
        while (L < n1 && L < n2 && L < n3 && s1[L] == s2[L] && s2[L] == s3[L]) {
            L++;
        }
        if (L == 0) return -1;
        return (n1 - L) + (n2 - L) + (n3 - L);
    }
};

int main() {
    string s1, s2, s3;
    cout << "Enter string s1: ";
    cin >> s1;
    cout << "Enter string s2: ";
    cin >> s2;
    cout << "Enter string s3: ";
    cin >> s3;
    Solution sol;
    cout << "Minimum operations: " << sol.findMinimumOperations(s1, s2, s3) << endl;
}
```
---

### **Java**
```Java
import java.util.*;

class Solution {
    public int findMinimumOperations(String s1, String s2, String s3) {
        int n1 = s1.length(), n2 = s2.length(), n3 = s3.length();
        int L = 0;
        while (L < n1 && L < n2 && L < n3 &&
               s1.charAt(L) == s2.charAt(L) &&
               s2.charAt(L) == s3.charAt(L)) {
            L++;
        }
        if (L == 0) return -1;
        return (n1 - L) + (n2 - L) + (n3 - L);
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter s1: ");
        String s1 = sc.next();
        System.out.print("Enter s2: ");
        String s2 = sc.next();
        System.out.print("Enter s3: ");
        String s3 = sc.next();
        Solution sol = new Solution();
        System.out.println("Minimum operations: " + sol.findMinimumOperations(s1, s2, s3));
    }
}


```
---

### **Pyhton**
```Pyhton
class Solution:
    def findMinimumOperations(self, s1: str, s2: str, s3: str) -> int:
        n1, n2, n3 = len(s1), len(s2), len(s3)
        L = 0
        while L < n1 and L < n2 and L < n3 and s1[L] == s2[L] == s3[L]:
            L += 1
        if L == 0:
            return -1
        return (n1 - L) + (n2 - L) + (n3 - L)

if __name__ == "__main__":
    s1 = input("Enter s1: ")
    s2 = input("Enter s2: ")
    s3 = input("Enter s3: ")
    sol = Solution()
    print("Minimum operations:", sol.findMinimumOperations(s1, s2, s3))

```
---

### **JavaScript**
```JavaScript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    findMinimumOperations(s1, s2, s3) {
        let n1 = s1.length, n2 = s2.length, n3 = s3.length;
        let L = 0;
        while (L < n1 && L < n2 && L < n3 &&
               s1[L] === s2[L] && s2[L] === s3[L]) {
            L++;
        }
        if (L === 0) return -1;
        return (n1 - L) + (n2 - L) + (n3 - L);
    }
}

readline.question("Enter s1: ", (s1) => {
    readline.question("Enter s2: ", (s2) => {
        readline.question("Enter s3: ", (s3) => {
            const sol = new Solution();
            console.log("Minimum operations:", sol.findMinimumOperations(s1, s2, s3));
            readline.close();
        });
    });
});
```
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

### **JavaScript**
```bash
node solution.js
```
---

## 🙏 Thanks
Thanks for checking out this repository ❤️  
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀  

---
