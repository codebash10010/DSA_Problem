# Bulb Switcher — (LeetCode: 319)

## 🏢 Companies Asked :- Amazon ✯, Google ✯, Microsoft ✯, Meta ✯

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

👉 [Problem Link](https://leetcode.com/problems/bulb-switcher/)

**Difficulty:** 🟡 Medium

---

## 🧩 Problem Statement

There are `n` bulbs that are initially turned off.
You first turn on all the bulbs, then you turn off every second bulb.
On the third round, you toggle every third bulb (turning it on if it's off or turning it off if it's on).
For the `i`-th round, you toggle every `i`-th bulb.

You need to return **the number of bulbs that remain on** after `n` rounds.

---

## 📌 Constraints

* `0 ≤ n ≤ 10⁹`

---

## 📌 Examples

### Example 1

**Input:**

```
n = 3
```

**Output:**

```
1
```

**Explanation:**

```
Initial: [off, off, off]
Round 1: [on, on, on]
Round 2: [on, off, on]
Round 3: [on, off, off]
→ Only bulb 1 is on
```

---

### Example 2

**Input:**

```
n = 0
```

**Output:**

```
0
```

---

### Example 3

**Input:**

```
n = 1
```

**Output:**

```
1
```

---

## 💡 Intuition

Each bulb toggles once for every factor (divisor) it has.

* For example, bulb `k` is toggled on rounds `i` where `i` divides `k`.
* Most numbers have **even** number of factors → they end **off**.
* Only **perfect squares** (like 1, 4, 9, 16, …) have **odd** number of factors → they end **on**.

Hence, the bulbs that remain **on** correspond to perfect squares ≤ `n`.

So, the answer is simply the **count of perfect squares ≤ n**,
which is `⌊√n⌋`.

---

## ⚙️ Approach (Step-by-Step)

1. Bulb `i` is toggled once for each of its divisors.
2. Only perfect squares have an odd number of divisors.
3. Thus, the bulbs at positions `1², 2², 3², …, k² ≤ n` remain on.
4. Return the integer part of `sqrt(n)`.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <iostream>
#include <cmath>
using namespace std;

int bulbSwitch(int n) {
    return sqrt(n);
}

int main() {
    int n;
    cin >> n;
    cout << bulbSwitch(n) << "\n";
    return 0;
}
```

---

### ☕ Java

```java
import java.util.*;

public class Main {
    public static int bulbSwitch(int n) {
        return (int)Math.sqrt(n);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        System.out.println(bulbSwitch(n));
        sc.close();
    }
}
```

---

### 🐍 Python

```python
import math

def bulbSwitch(n: int) -> int:
    return int(math.sqrt(n))

if __name__ == "__main__":
    n = int(input().strip())
    print(bulbSwitch(n))
```

---

### 🐍 JavaScript

```JavaScript
function bulbSwitch(n) {
  // The bulbs that are perfect squares remain on
  return Math.floor(Math.sqrt(n));
}

// Example with user input
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

readline.question("Enter number of bulbs (n): ", (line) => {
  const n = parseInt(line);
  console.log("Number of bulbs ON after all rounds:", bulbSwitch(n));
  readline.close();
});
```
---

## 🧪 Sample Runs

**Input**

```
3
```

**Output**

```
1
```

---

## ⏱ Complexity

* **Time Complexity:** O(1)
* **Space Complexity:** O(1)

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
