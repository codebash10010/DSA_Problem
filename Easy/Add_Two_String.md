# Add Strings — (LeetCode :- 415)

## 🏢 Companies Asked :- Amazon ✯, Google ✯, Microsoft ✯, Meta ✯

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
👉 [Problem Link](https://leetcode.com/problems/add-strings/)

**Difficulty:** 🟢 Easy

---


## 🧩 Problem Statement

You are given two non-negative integers, **num1** and **num2**, represented as **strings**. Return *the sum* of `num1` and `num2` **as a string**.

You must **not use any built-in library for large integers** (like `BigInteger` in Java) and you **cannot convert the inputs directly into integers**.

---

## 📌 Constraints

* `1 ≤ num1.length, num2.length ≤ 10⁴`
* `num1` and `num2` consist only of digits (`'0'`–`'9'`).
* `num1` and `num2` do not have leading zeros, except the number `0` itself. ([designgurus.io][2])

---

## 📌 Examples

### Example 1

**Input:**

```
num1 = "11", num2 = "123"
```

**Output:**

```
"134"
```

---

### Example 2

**Input:**

```
num1 = "456", num2 = "77"
```

**Output:**

```
"533"
```

---

### Example 3

**Input:**

```
num1 = "0", num2 = "0"
```

**Output:**

```
"0"
```

---

## 💡 Intuition

You can simulate the manual addition method you learned in school:

1. Add digits from the end (rightmost) toward the front (left).
2. Maintain a **carry**.
3. If one string is shorter, treat missing digits as `0`.
4. After processing all digits, if a carry remains, prepend it.

You build the result in **reverse order**, then reverse it at the end. ([walkccc.me][3])

---

## ⚙️ Approach (Step-by-Step)

1. Initialize pointers `i = num1.length - 1`, `j = num2.length - 1`.
2. Initialize `carry = 0` and a result container (e.g. `StringBuilder` or `vector<char>`).
3. Loop while `i >= 0` or `j >= 0` or `carry != 0`:

   * Let `a = (i >= 0 ? num1[i] - '0' : 0)`
   * Let `b = (j >= 0 ? num2[j] - '0' : 0)`
   * `sum = a + b + carry`
   * Append `(sum % 10)` to result
   * `carry = sum / 10`
   * Decrement `i`, `j`
4. Reverse the result and convert to string.

This approach works in `O(max(m, n))` time and uses `O(max(m, n))` additional space for the result. ([designgurus.io][2])

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <iostream>
#include <string>
#include <algorithm>
using namespace std;

string addStrings(const string &num1, const string &num2) {
    int i = num1.size() - 1;
    int j = num2.size() - 1;
    int carry = 0;
    string res;

    while (i >= 0 || j >= 0 || carry) {
        if (i >= 0) carry += (num1[i--] - '0');
        if (j >= 0) carry += (num2[j--] - '0');
        res.push_back(char('0' + (carry % 10)));
        carry /= 10;
    }

    reverse(res.begin(), res.end());
    return res;
}

int main() {
    string num1, num2;
    cin >> num1 >> num2;
    cout << addStrings(num1, num2) << "\n";
    return 0;
}
```

---

### ☕ Java

```java
import java.util.*;

public class Main {
    public static String addStrings(String num1, String num2) {
        int i = num1.length() - 1;
        int j = num2.length() - 1;
        int carry = 0;
        StringBuilder sb = new StringBuilder();

        while (i >= 0 || j >= 0 || carry != 0) {
            if (i >= 0) carry += num1.charAt(i--) - '0';
            if (j >= 0) carry += num2.charAt(j--) - '0';
            sb.append(carry % 10);
            carry /= 10;
        }

        return sb.reverse().toString();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String num1 = sc.next();
        String num2 = sc.next();
        System.out.println(addStrings(num1, num2));
        sc.close();
    }
}
```

---

### 🐍 Python

```python
def addStrings(num1: str, num2: str) -> str:
    i, j = len(num1) - 1, len(num2) - 1
    carry = 0
    result = []

    while i >= 0 or j >= 0 or carry:
        if i >= 0:
            carry += ord(num1[i]) - ord('0')
            i -= 1
        if j >= 0:
            carry += ord(num2[j]) - ord('0')
            j -= 1
        result.append(str(carry % 10))
        carry //= 10

    return ''.join(reversed(result))

if __name__ == "__main__":
    num1 = input().strip()
    num2 = input().strip()
    print(addStrings(num1, num2))
```

---

## 🧪 Sample Runs

**Input**

```
"456"
"77"
```

**Output**

```
"533"
```

---

## ⏱ Complexity

* **Time Complexity:** O(max(m, n))
* **Space Complexity:** O(max(m, n))

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