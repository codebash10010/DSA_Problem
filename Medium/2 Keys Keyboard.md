# 2 Keys Keyboard - (LeetCode :- 650)

## 🏢 Companies Asked :- Microsoft 
👉 [Watch on YouTube](https://www.youtube.com/watch?v=jNfZH3mdjOA) :contentReference[oaicite:0]{index=0}

---

## 🔗 Problem Link

You can find the original problem here:  
👉 https://leetcode.com/problems/2-keys-keyboard/ :contentReference[oaicite:1]{index=1}

---

## 📝 Problem Statement

You start with a notepad that initially contains **one character 'A'**.  

You can perform two operations:

1. **Copy All** — copies all the characters currently on the screen (you cannot copy a subset).  
2. **Paste** — pastes the characters copied in the most recent “Copy All” operation.

Given an integer `n`, return the **minimum number of operations** needed to get exactly `n` characters 'A' on the screen.

---

## 📌 Constraints

- `1 <= n <= 1000` (or similar constraints in problem)  
- Each operation (Copy All or Paste) counts as 1 step.  

---

## 📌 Examples

### Example 1  
**Input:** `n = 3`  
**Output:** `3`  
**Explanation:**  
- Step 1: Copy All (clipboard = “A”)  
- Step 2: Paste → “AA”  
- Step 3: Paste → “AAA”

---

### Example 2  
**Input:** `n = 1`  
**Output:** `0`  
**Explanation:** Already have 1 ‘A’, no operations needed.

---

## 💡 Intuition & Key Insight

- The operations essentially let you **multiply** your “A” count by pasting after copying.
- If you copy when you have `x` A’s, then paste `k` times, you end with `x * (k + 1)` A’s.
- To reach exactly `n`, you can think in reverse: **factorize** `n`, because each group of (copy + pastes) corresponds to a factor.
- The minimal operations correspond to **sum of prime factors** of `n`.

Why factorization works:

- Suppose `n = a * b`. You can first produce `a` A’s (in some minimal number of steps), then copy, then paste `b - 1` times to multiply by `b`. The cost for that multiplication is `b` (1 copy + `b-1` pastes).
- Therefore, you try all ways to factor `n`, choosing the minimal total operations.

Another perspective:  
Use dynamic programming or memoization:  
- `dp[i]` = minimum steps to get `i` A’s.  
- For every `i`, look for divisors `j` of `i`:  
  `dp[i] = dp[j] + (i/j)` when `i % j == 0`.  

Also, a greedy prime-factor approach is simpler and more efficient.

---

## ⏱ Complexity Analysis

- **Time Complexity:**  
  - Prime factorization approach: roughly `O(√n)`  
  - DP / memoization version: up to `O(n √n)` in worst case  
- **Space Complexity:** `O(n)` (for DP / memo storage) or `O(1)` for factorization approach  

---

## 💻 Implementations (with Driver Code)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int minSteps(int n) {
        int res = 0;
        int d = 2;
        while (n > 1) {
            while (n % d == 0) {
                res += d;
                n /= d;
            }
            d++;
        }
        return res;
    }
};

int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    Solution sol;
    cout << "Minimum operations: " << sol.minSteps(n) << endl;
    return 0;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public int minSteps(int n) {
        int res = 0;
        int d = 2;
        while (n > 1) {
            while (n % d == 0) {
                res += d;
                n /= d;
            }
            d++;
        }
        return res;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        Solution sol = new Solution();
        System.out.println("Minimum operations: " + sol.minSteps(n));
    }
}
```

---

### **Python**

```python
class Solution:
    def minSteps(self, n: int) -> int:
        res = 0
        d = 2
        while n > 1:
            while n % d == 0:
                res += d
                n //= d
            d += 1
        return res

if __name__ == "__main__":
    n = int(input("Enter n: "))
    sol = Solution()
    print("Minimum operations:", sol.minSteps(n))
```

---

### **JavaScript (Node.js)**

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

class Solution {
  minSteps(n) {
    let res = 0;
    let d = 2;
    while (n > 1) {
      while (n % d === 0) {
        res += d;
        n /= d;
      }
      d++;
    }
    return res;
  }
}

readline.question("Enter n: ", (nStr) => {
  let n = parseInt(nStr);
  const sol = new Solution();
  console.log("Minimum operations:", sol.minSteps(n));
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






