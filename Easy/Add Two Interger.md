# Add Two Integers (Using Bit Manipulation) — (LeetCode :- 2235)

## 🏢 Companies Asked :- Amazon ✯, Google ✯, Microsoft ✯, Meta ✯

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
👉 [Problem Link](https://leetcode.com/problems/add-two-integers/)

**Difficulty:** 🟢 Easy  

---

## 🧩 Problem Statement

Given two integers `num1` and `num2`, return *the sum of the two integers*, **without using the '+' or '-' operators**.

---

## 💡 Intuition

Normally we add two numbers using the `+` operator, but we can also simulate addition using **bitwise operations**.

* **XOR (`^`)** → gives the sum of bits without carrying.
* **AND (`&`)** → finds which bits will produce a carry.
* We then **left shift the carry (<< 1)** because a carry affects the next higher bit.

Repeat until no carry remains.

---

## ⚙️ Approach (Bit Manipulation Logic)

1. While `carry != 0`

   * `carry = (a & b) << 1` — find carry bits
   * `a = a ^ b` — add bits without carry
   * `b = carry` — add carry in the next iteration
2. Return `a`

---

## 🧠 Dry Run Example

Example:

```
num1 = 5 (0101)
num2 = 3 (0011)
```

| Step | a (num1) | b (num2) | Carry          | XOR Result | Next a | Next b |
| ---- | -------- | -------- | -------------- | ---------- | ------ | ------ |
| 1    | 0101     | 0011     | 0001<<1 = 0110 | 0110       | 0110   | 0110   |
| 2    | 0110     | 0110     | 0110<<1=1100   | 0000       | 0000   | 1100   |
| 3    | 0000     | 1100     | 0000           | 1100       | 1100   | 0000   |

Final Answer: `1100` → **8**

---

## 🧩 Code Implementations (with User Input)

---

### 🧱 C++

```cpp
#include <iostream>
using namespace std;

int add(int a, int b) {
    while (b != 0) {
        unsigned carry = (a & b) << 1; // carry bits
        a = a ^ b;                      // sum without carry
        b = carry;                      // carry added in next round
    }
    return a;
}

int main() {
    int a, b;
    cin >> a >> b;
    cout << add(a, b) << "\n";
    return 0;
}
```

---

### ☕ Java

```java
import java.util.*;

public class Main {
    public static int add(int a, int b) {
        while (b != 0) {
            int carry = (a & b) << 1;
            a = a ^ b;
            b = carry;
        }
        return a;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt(), b = sc.nextInt();
        System.out.println(add(a, b));
        sc.close();
    }
}
```

---

### 🐍 Python

```python
def add(a: int, b: int) -> int:
    mask = 0xFFFFFFFF
    while b != 0:
        carry = (a & b) << 1
        a = (a ^ b) & mask
        b = carry & mask
    return a if a <= 0x7FFFFFFF else ~(a ^ mask)

if __name__ == "__main__":
    a, b = map(int, input().split())
    print(add(a, b))
```

---

### ⚡ C

```c
#include <stdio.h>

int add(int a, int b) {
    while (b != 0) {
        unsigned carry = (a & b) << 1;
        a = a ^ b;
        b = carry;
    }
    return a;
}

int main() {
    int a, b;
    scanf("%d %d", &a, &b);
    printf("%d\n", add(a, b));
    return 0;
}
```

---

## 🧪 Sample Run

**Input**

```
5 3
```

**Output**

```
8
```

---

## ⏱ Complexity

* **Time Complexity:** O(1) — constant number of bit operations (32 times max)
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

### **JavaScript**
```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️  
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀  

---