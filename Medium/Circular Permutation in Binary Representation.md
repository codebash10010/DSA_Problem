# Circular Permutation in Binary Representation - (LeetCode :- 1238)

## 🏢 Companies Asked :- Google, Facebook, Microsoft

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/circular-permutation-in-binary-representation/description/)

---

## 🧩 Problem Statement

Given two integers `n` and `start`. Return any sequence `ans` of length `2^n` where:

* `ans[0] = start`.
* `ans[i]` and `ans[i+1]` differ by **exactly one bit**.
* `ans[0]` and `ans[2^n - 1]` differ by **exactly one bit**.

---

## 📌 Constraints

* `1 <= n <= 16`
* `0 <= start < 2^n`

---

## 📌 Example

### Example 1

Input: `n = 2, start = 3`
Output: `[3,2,0,1]`

### Example 2

Input: `n = 3, start = 2`
Output: `[2,3,1,0,4,5,7,6]`

---

## 💡 Intuition

Use **Gray code sequence** because consecutive numbers differ by exactly one bit. To start from `start`, XOR all numbers in standard Gray code with `start`.

---

## ⚙️ Approach

1. Generate standard Gray code sequence of size `2^n`.
2. XOR each element with `start` to rotate sequence to start at `start`.
3. Return the sequence.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<int> circularPermutation(int n, int start) {
    vector<int> res;
    int size = 1 << n;
    for (int i = 0; i < size; i++) {
        res.push_back(i ^ (i >> 1) ^ start);
    }
    return res;
}

int main() {
    int n, start;
    cin >> n >> start;
    vector<int> ans = circularPermutation(n, start);
    for (int x : ans) cout << x << " ";
    cout << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main {
    public static List<Integer> circularPermutation(int n, int start) {
        int size = 1 << n;
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < size; i++) {
            res.add((i ^ (i >> 1)) ^ start);
        }
        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int start = sc.nextInt();
        List<Integer> ans = circularPermutation(n, start);
        for (int x : ans) System.out.print(x + " ");
        System.out.println();
    }
}
```

### 🐍 Python

```python
def circularPermutation(n: int, start: int) -> list:
    return [i ^ (i >> 1) ^ start for i in range(1 << n)]

if __name__ == "__main__":
    n = int(input())
    start = int(input())
    print(*circularPermutation(n, start))
```

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

function circularPermutation(n, start) {
    const res = [];
    const size = 1 << n;
    for (let i = 0; i < size; i++) {
        res.push((i ^ (i >> 1)) ^ start);
    }
    return res;
}

readline.question("Enter n and start: ", (line) => {
    const [n, start] = line.split(" ").map(Number);
    console.log(circularPermutation(n, start).join(' '));
    readline.close();
});
```

---

## ⏱ Complexity

* **Time:** O(2^n)
* **Space:** O(2^n)

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
