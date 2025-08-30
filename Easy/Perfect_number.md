# Perfect Number - (LeetCode :- 507)
## Difficulty: 🌿 Easy  

## 🏢 Companies Asked :- Amazon 

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/perfect-number/

---

## 📝 Problem Statement

A **perfect number** is a positive integer that is equal to the sum of its positive divisors, excluding the number itself.  

Given an integer `num`, return `true` if `num` is a **perfect number**, otherwise return `false`.

---

## 📌 Constraints
- `1 <= num <= 10⁸`

---

## 📌 Examples

### **Example 1**
**Input:**  
`num = 28`  

**Output:**  
`true`  

**Explanation:** Divisors of 28 are `1, 2, 4, 7, 14`.  
Their sum is `1 + 2 + 4 + 7 + 14 = 28`.

---

### **Example 2**
**Input:**  
`num = 12`  

**Output:**  
`false`  

**Explanation:** Divisors are `1, 2, 3, 4, 6`.  
Sum = `16 ≠ 12`.

---

## 💡 Intuition Behind the Approach

- A divisor always comes in pairs.  
  For example, if `d` divides `num`, then `num / d` also divides `num`.  
- We can iterate only till `√num` to collect divisor pairs efficiently.  
- Exclude the number itself but include `1`.  

If the **sum of divisors** equals the number, it’s a **perfect number**.

---

## 📚 Algorithm

1. Handle edge case: if `num <= 1`, return `false`.  
2. Initialize `sum = 1` (since 1 is always a divisor).  
3. Loop from `2` to `√num`:  
   - If `i` divides `num`, add both `i` and `num / i` to `sum`.  
4. After loop, check if `sum == num`.  

**Time Complexity:** `O(√n)`  
**Space Complexity:** `O(1)`

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <cmath>
using namespace std;

class Solution {
public:
    bool checkPerfectNumber(int num) {
        if (num <= 1) return false;
        int sum = 1;
        for (int i = 2; i <= sqrt(num); i++) {
            if (num % i == 0) {
                sum += i;
                if (i != num / i) sum += num / i;
            }
        }
        return sum == num;
    }
};

int main() {
    int n; cin >> n;
    Solution sol;
    cout << (sol.checkPerfectNumber(n) ? "true" : "false");
}

```
---

### Java

```java
import java.util.*;

class Solution {
    public boolean checkPerfectNumber(int num) {
        if (num <= 1) return false;
        int sum = 1;
        for (int i = 2; i * i <= num; i++) {
            if (num % i == 0) {
                sum += i;
                if (i != num / i) sum += num / i;
            }
        }
        return sum == num;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Solution sol = new Solution();
        System.out.println(sol.checkPerfectNumber(n));
    }
}


```

---

### Python

```python
import math

class Solution:
    def checkPerfectNumber(self, num: int) -> bool:
        if num <= 1:
            return False
        total = 1
        for i in range(2, int(math.sqrt(num)) + 1):
            if num % i == 0:
                total += i
                if i != num // i:
                    total += num // i
        return total == num

if __name__ == "__main__":
    n = int(input())
    sol = Solution()
    print(sol.checkPerfectNumber(n))

```

---

### JavaScript 

```javascript
class Solution {
    checkPerfectNumber(num) {
        if (num <= 1) return false;
        let sum = 1;
        for (let i = 2; i * i <= num; i++) {
            if (num % i === 0) {
                sum += i;
                if (i !== num / i) sum += num / i;
            }
        }
        return sum === num;
    }
}

// Driver
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question("Enter number: ", (nStr) => {
    const n = parseInt(nStr);
    const sol = new Solution();
    console.log(sol.checkPerfectNumber(n));
    readline.close();
});


```

---

## 🧪 Tests You Can Try

Input: 28
Output: true

Input: 12
Output: false

Input: 6
Output: true

Input: 496
Output: true

Input: 25
Output: false

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

