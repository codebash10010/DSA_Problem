#  4 Keys Keyboard - (LeetCode :- 651)

## 🏢 Companies Asked :- DoorDash✯, TikTok✯, Facebook✯, Amazon✯, Adobe✯, Google, Goldman Sachs, Microsoft, Apple, DE Shaw, Bloomberg

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium  

👉 [Problem Link](https://leetcode.com/problems/4-keys-keyboard/)  

---

## 📝 Problem Statement

You have a special keyboard with **4 keys**:

1. **Key 1 (A):** Prints one 'A' on the screen.  
2. **Key 2 (Ctrl-A):** Selects all the text on the screen.  
3. **Key 3 (Ctrl-C):** Copies the selected text to the buffer.  
4. **Key 4 (Ctrl-V):** Pastes the buffer content—appending it to what’s already on screen.

You can press keys exactly **N** times.  
Return the **maximum number of 'A'** you can have on the screen after N key presses.

---

## 📌 Constraints

- `1 <= N <= 50` :contentReference[oaicite:1]{index=1}  
- Answers fit within a 32-bit signed integer :contentReference[oaicite:2]{index=2}  

---

## 📌 Examples

### Example 1  
**Input:** `N = 3`  
**Output:** `3`  
**Explanation:** Press `A, A, A`.

---

### Example 2  
**Input:** `N = 7`  
**Output:** `9`  
**Explanation:** One optimal sequence: `A, A, A, Ctrl-A, Ctrl-C, Ctrl-V, Ctrl-V` → “AAA” then double and paste → 9.

---

## 💡 Intuition & Approach

- If `N` is small (≤ 6), the best you can do is just press `A` every time → you get `N` 'A's.  
- For larger `N`, the benefit comes from **copy-paste sequences**.  
- The optimal sequence generally ends with a block: `Ctrl-A`, `Ctrl-C`, then many `Ctrl-V`s.  
- You can try at each point `j` (where you initiate the copy) the result:  
```

dp[j-1] * (N - (j - 1) - 1)

````
which means: you had `dp[j-1]` 'A's, then use up one step for Ctrl-A, one for Ctrl-C, and paste for the rest.  
- Use dynamic programming:  
- `dp[i]` = maximum 'A's with `i` presses  
- Initialize `dp[i] = i` (all presses as `A`)  
- For each `i`, try all possible breakpoints `j` and update `dp[i] = max(dp[i], dp[j-2] * (i - j + 1))`

This approach runs in `O(N²)` time with `O(N)` space. :contentReference[oaicite:3]{index=3}  

---

## 💻 Implementations (with User Input)

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxA(int N) {
  vector<long long> dp(N + 1);
  for (int i = 0; i <= N; i++) dp[i] = i;
  for (int i = 3; i <= N; i++) {
      for (int j = 1; j <= i - 2; j++) {
          long long current = dp[j] * (i - j - 1);
          dp[i] = max(dp[i], current);
      }
  }
  return dp[N];
}

int main() {
  int N;
  cout << "Enter N (number of key presses): ";
  cin >> N;
  cout << "Maximum A's: " << maxA(N) << endl;
  return 0;
}
````

---

### **Java**

```java
import java.util.*;

public class Main {
    public static int maxA(int N) {
        long[] dp = new long[N + 1];
        for (int i = 0; i <= N; i++) dp[i] = i;
        for (int i = 3; i <= N; i++) {
            for (int j = 1; j <= i - 2; j++) {
                long curr = dp[j] * (i - j - 1);
                dp[i] = Math.max(dp[i], curr);
            }
        }
        return (int) dp[N];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter N (number of key presses): ");
        int N = sc.nextInt();
        System.out.println("Maximum A's: " + maxA(N));
    }
}
```

---

### **Python**

```python
def maxA(N: int) -> int:
    dp = [i for i in range(N + 1)]
    for i in range(3, N + 1):
        for j in range(1, i - 1):
            dp[i] = max(dp[i], dp[j] * (i - j - 1))
    return dp[N]

if __name__ == "__main__":
    N = int(input("Enter N (number of key presses): "))
    print("Maximum A's:", maxA(N))
```

---

### **JavaScript (Node.js)**

```javascript
function maxA(N) {
    const dp = Array(N + 1).fill(0).map((_, i) => i);
    for (let i = 3; i <= N; i++) {
        for (let j = 1; j <= i - 2; j++) {
            dp[i] = Math.max(dp[i], dp[j] * (i - j - 1));
        }
    }
    return dp[N];
}

const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout
});
readline.question("Enter N (number of key presses): ", (str) => {
    const N = parseInt(str);
    console.log("Maximum A's:", maxA(N));
    readline.close();
});
```

---

## 🧪 Sample Test Cases

| N | Output | Explanation                                   |
| - | ------ | --------------------------------------------- |
| 3 | 3      | Just press `A` thrice                         |
| 7 | 9      | Use `A, A, A, Ctrl-A, Ctrl-C, Ctrl-V, Ctrl-V` |
| 1 | 1      | Only `A`                                      |

---

## ⏱ Complexity

* Time Complexity: **O(N²)**
* Space Complexity: **O(N)**

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
