Perfect 👍 Here's the **complete and final `.md` file** for **LeetCode 672 – Bulb Switcher II**, now with **C++, Java, Python, and JavaScript** implementations 👇

---

# Bulb Switcher II — (LeetCode :- 672)

## 🏢 Companies Asked :- Microsoft ✯, Amazon ✯, Google ✯, Adobe ✯, Meta ✯, Apple ✯

👉 [Watch on YouTube](https://www.youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

👉 [Problem Link](https://leetcode.com/problems/bulb-switcher-ii/)

**Difficulty:** 🟡 Medium

---

## 🧩 Problem Statement

There is a room with **n bulbs** labeled from 1 to n, all initially **ON**.
There are **4 buttons**. Each button toggles (flips) certain bulbs:

1. **Button 1:** Flips the status of **all bulbs**
2. **Button 2:** Flips **even-labeled bulbs** (2, 4, 6, …)
3. **Button 3:** Flips **odd-labeled bulbs** (1, 3, 5, …)
4. **Button 4:** Flips bulbs with labels `3k + 1` → (1, 4, 7, 10, …)

You must press exactly `presses` times (you can press any button each time, including repeating).
Return the number of **distinct possible bulb configurations** after all presses.

---

## 📌 Constraints

* `1 ≤ n, presses ≤ 1000`
* The pattern for large `n` repeats due to periodic toggles, so we only need to consider the first 6 bulbs.

---

## 📌 Examples

### Example 1

**Input:**

```
n = 1, presses = 1
```

**Output:**

```
2
```

---

### Example 2

**Input:**

```
n = 2, presses = 1
```

**Output:**

```
3
```

---

### Example 3

**Input:**

```
n = 3, presses = 1
```

**Output:**

```
4
```

---

## 💡 Intuition

Each button toggles bulbs in a specific pattern.
If you press the same button twice, it cancels out its effect.
Hence, we only care whether each button is pressed **odd** or **even** times.

There are **4 buttons → 2⁴ = 16** possible toggle combinations.
We filter them based on:

* Number of pressed buttons ≤ `presses`
* Parity (`count_of_pressed % 2 == presses % 2`)

Since bulb behavior repeats after 6 bulbs, we only need to simulate the first 6.

---

## ⚙️ Approach (Step-by-Step)

1. Reduce `n` to `min(n, 6)` to handle repetition.
2. Represent bulb states as 6-bit integers.
3. For each combination of button presses (0 to 15):

   * Count number of buttons pressed.
   * Skip if invalid (based on presses count and parity).
   * XOR the masks of pressed buttons to simulate toggles.
   * Store resulting patterns in a set.
4. The answer is the number of unique states in the set.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int flipLights(int n, int presses) {
    n = min(n, 6);
    vector<int> ops = {
        0b111111,  // flip all
        0b010101,  // flip even
        0b101010,  // flip odd
        0b100100   // flip 3k+1
    };
    unordered_set<int> seen;
    for (int mask = 0; mask < (1 << 4); mask++) {
        int cnt = __builtin_popcount(mask);
        if (cnt > presses || (cnt % 2) != (presses % 2)) continue;
        int state = 0;
        for (int i = 0; i < 4; i++) {
            if (mask & (1 << i)) state ^= ops[i];
        }
        state >>= (6 - n);
        seen.insert(state);
    }
    return seen.size();
}

int main() {
    int n, presses;
    cin >> n >> presses;
    cout << flipLights(n, presses) << "\n";
    return 0;
}
```

---

### ☕ Java

```java
import java.util.*;

public class Main {
    public static int flipLights(int n, int presses) {
        n = Math.min(n, 6);
        int[] ops = {
            0b111111,  // flip all
            0b010101,  // flip even
            0b101010,  // flip odd
            0b100100   // flip 3k+1
        };
        Set<Integer> seen = new HashSet<>();
        for (int mask = 0; mask < (1 << 4); mask++) {
            int cnt = Integer.bitCount(mask);
            if (cnt > presses || (cnt % 2) != (presses % 2)) continue;
            int state = 0;
            for (int i = 0; i < 4; i++) {
                if ((mask & (1 << i)) != 0) state ^= ops[i];
            }
            state >>= (6 - n);
            seen.add(state);
        }
        return seen.size();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int presses = sc.nextInt();
        System.out.println(flipLights(n, presses));
        sc.close();
    }
}
```

---

### 🐍 Python

```python
def flipLights(n: int, presses: int) -> int:
    n = min(n, 6)
    ops = [
        0b111111,  # flip all
        0b010101,  # flip even
        0b101010,  # flip odd
        0b100100   # flip 3k+1
    ]
    seen = set()
    for mask in range(1 << 4):
        cnt = bin(mask).count('1')
        if cnt > presses or (cnt % 2) != (presses % 2):
            continue
        state = 0
        for i in range(4):
            if (mask >> i) & 1:
                state ^= ops[i]
        state >>= (6 - n)
        seen.add(state)
    return len(seen)

if __name__ == "__main__":
    n, presses = map(int, input().split())
    print(flipLights(n, presses))
```

---

### 💻 JavaScript

```javascript
function flipLights(n, presses) {
  n = Math.min(n, 6);
  const ops = [
    0b111111, // flip all
    0b010101, // flip even
    0b101010, // flip odd
    0b100100  // flip 3k+1
  ];

  const seen = new Set();

  for (let mask = 0; mask < (1 << 4); mask++) {
    const cnt = mask.toString(2).split('1').length - 1;
    if (cnt > presses || cnt % 2 !== presses % 2) continue;
    let state = 0;
    for (let i = 0; i < 4; i++) {
      if (mask & (1 << i)) state ^= ops[i];
    }
    state >>= (6 - n);
    seen.add(state);
  }

  return seen.size;
}

// Example with user input simulation:
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

readline.question("", (line) => {
  const [n, presses] = line.split(" ").map(Number);
  console.log(flipLights(n, presses));
  readline.close();
});
```

---

## 🧪 Sample Run

**Input**

```
3 1
```

**Output**

```
4
```

---

## ⏱ Complexity

| Complexity   | Explanation                   |
| ------------ | ----------------------------- |
| ⏰ **Time**   | `O(1)` (only 16 combinations) |
| 💾 **Space** | `O(1)` (constant states)      |

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

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---