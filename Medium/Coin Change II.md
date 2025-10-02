# Coin Change II - (LeetCode :- 518)

## 🏢 Companies Asked :- Amazon , Microsoft , Google , Adobe , Facebook  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/coin-change-2/description/

---

## 📝 Problem Statement

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.  

Return the **number of combinations** that make up that amount.  

You may assume that you have an **infinite number of each kind of coin**.  

---

## 📌 Constraints
- `1 <= coins.length <= 300`
- `1 <= coins[i] <= 5000`
- `0 <= amount <= 5000`
- The answer is guaranteed to fit into a signed 32-bit integer.

---

## 📌 Examples

### Example 1
**Input:**  
`amount = 5, coins = [1,2,5]`  

**Output:**  
`4`  

**Explanation:**  
There are four ways to make up the amount:  
- 5 = 5  
- 5 = 2 + 2 + 1  
- 5 = 2 + 1 + 1 + 1  
- 5 = 1 + 1 + 1 + 1 + 1  

---

### Example 2
**Input:**  
`amount = 3, coins = [2]`  

**Output:**  
`0`  

---

### Example 3
**Input:**  
`amount = 10, coins = [10]`  

**Output:**  
`1`  

---

## 💡 Intuition Behind the Approach

This is a **classic dynamic programming (DP)** problem:  

👉 **Key Idea:**  
We want the number of **combinations**, not permutations.  
So, order does **not** matter.  

1. Use **1D DP array**, where `dp[i]` = number of ways to make amount `i`.  
2. Initialize: `dp[0] = 1` (base case → one way to make `0`, by choosing nothing).  
3. For each `coin`:  
   - Traverse amounts from `coin` to `amount`.  
   - Update `dp[i] += dp[i - coin]`.  

This ensures combinations (not permutations), since we iterate **coins first**.  

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(amount × n)` where `n` = number of coins.  
- **Space Complexity:** `O(amount)`  

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int> dp(amount + 1, 0);
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        return dp[amount];
    }
};

int main() {
    int n, amount;
    cout << "Enter number of coins: ";
    cin >> n;
    vector<int> coins(n);
    cout << "Enter coin denominations: ";
    for (int i = 0; i < n; i++) cin >> coins[i];
    cout << "Enter amount: ";
    cin >> amount;
    Solution sol;
    cout << "Number of combinations: " << sol.change(amount, coins) << endl;
    return 0;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        return dp[amount];
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of coins: ");
        int n = sc.nextInt();
        int[] coins = new int[n];
        System.out.println("Enter coin denominations:");
        for (int i = 0; i < n; i++) coins[i] = sc.nextInt();
        System.out.print("Enter amount: ");
        int amount = sc.nextInt();
        Solution sol = new Solution();
        System.out.println("Number of combinations: " + sol.change(amount, coins));
    }
}
```

---

### **Python**

```python
class Solution:
    def change(self, amount, coins):
        dp = [0] * (amount + 1)
        dp[0] = 1
        for coin in coins:
            for i in range(coin, amount + 1):
                dp[i] += dp[i - coin]
        return dp[amount]

if __name__ == "__main__":
    n = int(input("Enter number of coins: "))
    coins = list(map(int, input("Enter coin denominations: ").split()))
    amount = int(input("Enter amount: "))
    sol = Solution()
    print("Number of combinations:", sol.change(amount, coins))
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    change(amount, coins) {
        let dp = new Array(amount + 1).fill(0);
        dp[0] = 1;
        for (let coin of coins) {
            for (let i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        return dp[amount];
    }
}

readline.question("Enter number of coins: ", (nStr) => {
    readline.question("Enter coin denominations (space-separated): ", (arrStr) => {
        readline.question("Enter amount: ", (amtStr) => {
            let coins = arrStr.trim().split(" ").map(Number);
            let amount = parseInt(amtStr);
            const sol = new Solution();
            console.log("Number of combinations:", sol.change(amount, coins));
            readline.close();
        });
    });
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

If this helped you, please ⭐ the repo & share it ❤️🚀

```

---

Do you want me to prepare the **same structure `.md`** next for **Coin Change I (LeetCode 322)** as well, so you have both problems side by side?
```
