# Count Special Integers - (LeetCode :- 2376)

## Difficulty: 🔴 Hard

## 🏢 Companies Asked :- Google, Amazon, Microsoft, Adobe

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:  
👉 https://leetcode.com/problems/count-special-integers/

---

## 📝 Problem Statement

We call a **positive integer special** if **all of its digits are distinct**.

Given a positive integer `n`, return the number of **special integers** that belong to the interval `[1, n]`.

---

## 📌 Constraints

- `1 <= n <= 2 * 10⁹`

---

## 📌 Examples

### Example 1

**Input:**  
n = 20

**Output:**  
19

**Explanation:**  
All numbers from 1 → 20 are special except **11**.  
Hence, count = 19.

---

### Example 2

**Input:**  
n = 5

**Output:**  
5

**Explanation:**  
Numbers `1, 2, 3, 4, 5` are all distinct → special.

---

### Example 3

**Input:**  
n = 135

**Output:**  
110

**Explanation:**  
Some invalid (non-special) numbers: `22, 114, 131` (because of repeating digits).  
Hence, total special integers = 110.

---

## 💡 Intuition Behind the Approach

👉 A number is **not special** if any digit repeats.

To solve efficiently:

1. **Digit DP (Dynamic Programming on Digits):**

   - Traverse digits of `n` left → right.
   - Track:
     - `index` (current digit index).
     - `mask` (bitmask of used digits).
     - `tight` (whether we are still following the prefix of n).
     - `started` (whether we have started forming the number).

2. **Transitions:**
   - Try placing each valid digit that is not already used.
   - If placing this digit keeps number ≤ `n`, continue.
   - Avoid leading zero issues with `started`.

✅ This counts all **special integers ≤ n**.

**Time Complexity:** `O(digits * 2^digits)` (≈ 10 _ 1024 = 10k states).  
**Space Complexity:** `O(digits _ 2^digits)` for memoization.

---

## 📚 Algorithm Steps

1. Convert `n` to string for digit access.
2. Use recursive DP with memoization.
3. Base case: if we finish all digits, return 1 if we placed at least one digit.
4. For each position, iterate over possible digits (0–9).
5. Skip digits that are already used.
6. Handle tight bound (cannot exceed `n`).
7. Return total count.

---

## 💻 Implementations

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    string num;
    int dp[11][1<<10][2][2];

    int solve(int idx, int mask, bool tight, bool started) {
        if (idx == num.size()) return started ? 1 : 0;
        if (dp[idx][mask][tight][started] != -1) return dp[idx][mask][tight][started];

        int limit = tight ? num[idx] - '0' : 9;
        int ans = 0;

        for (int d = 0; d <= limit; d++) {
            if ((mask & (1 << d)) && started) continue;
            int newMask = (started || d != 0) ? (mask | (1 << d)) : mask;
            bool newStarted = started || (d != 0);
            ans += solve(idx+1, newMask, tight && (d == limit), newStarted);
        }
        return dp[idx][mask][tight][started] = ans;
    }

    int countSpecialNumbers(int n) {
        num = to_string(n);
        memset(dp, -1, sizeof(dp));
        return solve(0, 0, 1, 0);
    }
};

// Driver
int main() {
    Solution sol;
    int n;
    cout << "Enter n: ";
    cin >> n;
    cout << "Special integers <= " << n << " = " << sol.countSpecialNumbers(n) << endl;
}
```

---

### Java

```java
import java.util.*;

class Solution {
    String num;
    Integer[][][][] dp;

    int dfs(int idx, int mask, int tight, int started) {
        if (idx == num.length()) return started == 1 ? 1 : 0;
        if (dp[idx][mask][tight][started] != null) return dp[idx][mask][tight][started];

        int limit = (tight == 1) ? num.charAt(idx) - '0' : 9;
        int ans = 0;

        for (int d = 0; d <= limit; d++) {
            if ((mask & (1 << d)) != 0 && started == 1) continue;
            int newMask = (started == 1 || d != 0) ? (mask | (1 << d)) : mask;
            int newStarted = (started == 1 || d != 0) ? 1 : 0;
            int newTight = (tight == 1 && d == limit) ? 1 : 0;
            ans += dfs(idx+1, newMask, newTight, newStarted);
        }
        return dp[idx][mask][tight][started] = ans;
    }

    public int countSpecialNumbers(int n) {
        num = String.valueOf(n);
        dp = new Integer[12][1<<10][2][2];
        return dfs(0, 0, 1, 0);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Solution sol = new Solution();
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        System.out.println("Special integers <= " + n + " = " + sol.countSpecialNumbers(n));
    }
}

```

---

### Python

```python
from functools import lru_cache

class Solution:
    def countSpecialNumbers(self, n: int) -> int:
        num = str(n)

        @lru_cache(None)
        def dfs(idx, mask, tight, started):
            if idx == len(num):
                return 1 if started else 0

            limit = int(num[idx]) if tight else 9
            ans = 0
            for d in range(limit+1):
                if started and (mask >> d) & 1:
                    continue
                newMask = (mask | (1 << d)) if (started or d != 0) else mask
                newStarted = started or d != 0
                newTight = tight and (d == limit)
                ans += dfs(idx+1, newMask, newTight, newStarted)
            return ans

        return dfs(0, 0, True, False)

# Driver
if __name__ == "__main__":
    n = int(input("Enter n: "))
    sol = Solution()
    print("Special integers <=", n, "=", sol.countSpecialNumbers(n))


```

---

### JavaScript

```javascript
class Solution {
  countSpecialNumbers(n) {
    const num = n.toString();
    const dp = new Map();

    const dfs = (idx, mask, tight, started) => {
      if (idx === num.length) return started ? 1 : 0;
      const key = `${idx},${mask},${tight},${started}`;
      if (dp.has(key)) return dp.get(key);

      let limit = tight ? Number(num[idx]) : 9;
      let ans = 0;
      for (let d = 0; d <= limit; d++) {
        if (started && mask & (1 << d)) continue;
        let newMask = started || d !== 0 ? mask | (1 << d) : mask;
        let newStarted = started || d !== 0;
        let newTight = tight && d === limit;
        ans += dfs(idx + 1, newMask, newTight, newStarted);
      }
      dp.set(key, ans);
      return ans;
    };
    return dfs(0, 0, true, false);
  }
}

// Driver
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});
readline.question("Enter n: ", (nStr) => {
  const n = parseInt(nStr);
  const sol = new Solution();
  console.log("Special integers <=", n, "=", sol.countSpecialNumbers(n));
  readline.close();
});
```

---

## 🧪 Tests You Can Try

Input: 20
Output: 19

Input: 5
Output: 5

Input: 135
Output: 110

Input: 1000
Output: 738

Input: 9999
Output: 4536

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
