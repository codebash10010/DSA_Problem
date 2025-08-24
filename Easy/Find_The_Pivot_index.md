# Find the Pivot Integer - (LeetCode :- 2485)

## 🏢 Companies Asked :- Amazon, Google, Microsoft  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/find-the-pivot-integer/

---

## 📝 Problem Statement

Given a positive integer `n`, find the **pivot integer `x`** such that:  

**Sum(1 … x) = Sum(x … n)**  

If no such integer exists, return `-1`.  

It is guaranteed that there will be **at most one** pivot index for the given input.

---

## 📌 Constraints
- `1 <= n <= 1000`

---

## 📌 Examples

### **Example 1**
**Input:**  
n = 8


**Output:**  

6

**Explanation:**  

1 + 2 + 3 + 4 + 5 + 6 = 21
6 + 7 + 8 = 21

So, `x = 6`.

---

### **Example 2**
**Input:**  

n = 1

**Output:**  

1

**Explanation:**  
1 = 1

---

### **Example 3**
**Input:**  

n = 4

**Output:**  
-1

---


**Explanation:**  
No integer between `1` and `4` satisfies the condition.  

---

## 💡 Intuition Behind the Approach

We want to find an integer `x` such that:  

**Sum(1 … x) = Sum(x … n)**  

👉 That means:  

(1 + 2 + … + x) = (x + (x+1) + … + n)

Let total = sum(1 … n) = `n*(n+1)/2`.

Then condition becomes:  

sum(1 … x) = total - sum(1 … (x-1))


## Simplify: 

x*(x+1)/2 = total - (x*(x-1))/2


If this equality holds → `x` is the pivot.  

---

## 📚 Algorithm Explanation

1. Compute total sum = `n*(n+1)/2`.  
2. Iterate over possible `x` from `1` to `n`.  
3. For each `x`, compute prefix = `x*(x+1)/2`.  
   - If prefix == total - prefix + x → return `x`.  
4. If no such `x` found, return `-1`.  

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`  

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
using namespace std;

class Solution {
public:
    int pivotInteger(int n) {
        int total = n * (n + 1) / 2;
        for (int x = 1; x <= n; x++) {
            int left = x * (x + 1) / 2;
            int right = total - left + x;
            if (left == right) return x;
        }
        return -1;
    }
};

int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    Solution sol;
    cout << "Pivot Integer: " << sol.pivotInteger(n) << endl;
}
```
---

### **Java**
```Java
import java.util.*;

class Solution {
    public int pivotInteger(int n) {
        int total = n * (n + 1) / 2;
        for (int x = 1; x <= n; x++) {
            int left = x * (x + 1) / 2;
            int right = total - left + x;
            if (left == right) return x;
        }
        return -1;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        Solution sol = new Solution();
        System.out.println("Pivot Integer: " + sol.pivotInteger(n));
    }
}

```
---

### **Pyhton**
```Pyhton
class Solution:
    def pivotInteger(self, n: int) -> int:
        total = n * (n + 1) // 2
        for x in range(1, n + 1):
            left = x * (x + 1) // 2
            right = total - left + x
            if left == right:
                return x
        return -1

if __name__ == "__main__":
    n = int(input("Enter n: "))
    sol = Solution()
    print("Pivot Integer:", sol.pivotInteger(n))
```
---

### **JavaScript**
```JavaScript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    pivotInteger(n) {
        const total = n * (n + 1) / 2;
        for (let x = 1; x <= n; x++) {
            const left = x * (x + 1) / 2;
            const right = total - left + x;
            if (left === right) return x;
        }
        return -1;
    }
}

readline.question("Enter n: ", (nStr) => {
    const n = parseInt(nStr);
    const sol = new Solution();
    console.log("Pivot Integer:", sol.pivotInteger(n));
    readline.close();
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