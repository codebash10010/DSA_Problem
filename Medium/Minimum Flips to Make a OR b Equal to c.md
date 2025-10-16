# Minimum Flips to Make A OR B Equal to C - (LeetCode :- 1318)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Facebook

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/minimum-flips-to-make-a-or-b-equal-to-c/)

---

## 🧩 Problem Statement

Given **three positive integers** `a`, `b`, and `c`, return the **minimum number of flips** required in **`a` and `b`** to make `(a OR b == c)`.

A **flip** consists of changing any bit `0` to `1` or `1` to `0` in the **binary representation** of `a` or `b`.

---

## 📌 Constraints

* `1 <= a, b, c <= 10^9`

---

## 📌 Example

### Example 1

Input: `a = 2, b = 6, c = 5`
Output: `3`

Explanation:

```
a = 010
b = 110
c = 101

Flip a's 2nd bit: 010 -> 000
Flip b's 3rd bit: 110 -> 100
Flip b's 1st bit: 100 -> 101
Total flips = 3
```

### Example 2

Input: `a = 4, b = 2, c = 7`
Output: `1`

---

## 💡 Intuition

Compare each bit of `a`, `b`, and `c`.

Rules:

1. If `c_bit == 0` → Both `a_bit` and `b_bit` must be `0`. Count flips needed to turn `1`s to `0`s.
2. If `c_bit == 1` → At least one of `a_bit` or `b_bit` must be `1`. Count flips if both are `0`.

---

## ⚙️ Approach (Bit Manipulation)

1. Initialize `flips = 0`.
2. Loop while any of `a`, `b`, `c` > 0:

   * Extract lowest bit of `a`, `b`, `c`: `a_bit = a & 1`, `b_bit = b & 1`, `c_bit = c & 1`.
   * Apply the rules above to increment `flips`.
   * Right shift `a`, `b`, `c`.
3. Return `flips`.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int minFlips(int a, int b, int c) {
    int flips = 0;
    while(a || b || c){
        int a_bit = a & 1, b_bit = b & 1, c_bit = c & 1;
        if(c_bit == 0){
            flips += a_bit + b_bit;
        } else {
            if(a_bit == 0 && b_bit == 0) flips += 1;
        }
        a >>= 1;
        b >>= 1;
        c >>= 1;
    }
    return flips;
}

int main(){
    int a,b,c;
    cin >> a >> b >> c;
    cout << minFlips(a,b,c) << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main {
    public static int minFlips(int a, int b, int c) {
        int flips = 0;
        while(a != 0 || b != 0 || c != 0){
            int a_bit = a & 1, b_bit = b & 1, c_bit = c & 1;
            if(c_bit == 0) flips += a_bit + b_bit;
            else if(a_bit == 0 && b_bit == 0) flips += 1;
            a >>= 1; b >>= 1; c >>= 1;
        }
        return flips;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        int c = sc.nextInt();
        System.out.println(minFlips(a,b,c));
        sc.close();
    }
}
```

### 🐍 Python

```python
def minFlips(a: int, b: int, c: int) -> int:
    flips = 0
    while a or b or c:
        a_bit = a & 1
        b_bit = b & 1
        c_bit = c & 1
        if c_bit == 0:
            flips += a_bit + b_bit
        elif a_bit == 0 and b_bit == 0:
            flips += 1
        a >>= 1
        b >>= 1
        c >>= 1
    return flips

if __name__=="__main__":
    a,b,c=map(int,input().split())
    print(minFlips(a,b,c))
```

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

function minFlips(a, b, c) {
    let flips = 0;
    while(a || b || c){
        let a_bit = a & 1, b_bit = b & 1, c_bit = c & 1;
        if(c_bit === 0) flips += a_bit + b_bit;
        else if(a_bit === 0 && b_bit === 0) flips += 1;
        a >>= 1; b >>= 1; c >>= 1;
    }
    return flips;
}

readline.question("Enter a b c: ", line=>{
    const [a,b,c]=line.split(' ').map(Number);
    console.log(minFlips(a,b,c));
    readline.close();
});
```

---

## ⏱ Complexity

* **Time:** O(32) → O(1), since integers are 32-bit.
* **Space:** O(1)

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

### **JavaScript**

```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀
