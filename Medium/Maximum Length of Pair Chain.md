# Maximum Length of Pair Chain - (LeetCode :- 646)

## 🏢 Companies Asked :- Josh

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:
👉 [https://leetcode.com/problems/maximum-length-of-pair-chain/](https://leetcode.com/problems/maximum-length-of-pair-chain/)

---

## 📝 Problem Statement

You are given an array of `n` pairs `pairs` where `pairs[i] = [lefti, righti]` and `lefti < righti`.

A pair `[c, d]` can follow another pair `[a, b]` if and only if `b < c`.

A chain of pairs can be formed in this way.

Return the **length of the longest chain** which can be formed.

You do not need to use up all the given pairs. You can select pairs in any order.

---

## 📌 Constraints

* `1 <= pairs.length <= 1000`
* `-1000 <= lefti < righti <= 1000`

---

## 📌 Examples

### **Example 1**

**Input:**
pairs = [[1,2],[2,3],[3,4]]

**Output:**
2

**Explanation:**
The longest chain is `[1,2] -> [3,4]`.

---

### **Example 2**

**Input:**
pairs = [[1,2],[7,8],[4,5]]

**Output:**
3

**Explanation:**
The longest chain is `[1,2] -> [4,5] -> [7,8]`.

---

## 💡 Intuition Behind the Approach

We need to form the **maximum chain of pairs** such that the next pair starts only after the previous one ends.

👉 This is similar to the **Activity Selection Problem** or **Interval Scheduling**.

**Steps:**

1. Sort pairs by their **end value** (`righti`).
2. Greedily select pairs where the current pair’s `left` is greater than the last chosen pair’s `right`.
3. Count how many pairs can be chained this way.

This greedy approach ensures maximum length.

---

## 📚 Algorithm Explanation

1. Sort the pairs by their second element.
2. Initialize `count = 0` and `currEnd = -∞`.
3. For each pair:

   * If `pair[0] > currEnd`, then include this pair in chain → `count++`, update `currEnd = pair[1]`.
4. Return `count`.

**Time Complexity:** `O(n log n)` (for sorting)
**Space Complexity:** `O(1)`

---

## 💻 Implementations

### **C++**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

class Solution {
public:
    int findLongestChain(vector<vector<int>>& pairs) {
        sort(pairs.begin(), pairs.end(), [](auto &a, auto &b){
            return a[1] < b[1];
        });
        int count = 0, currEnd = INT_MIN;
        for (auto &p : pairs) {
            if (p[0] > currEnd) {
                count++;
                currEnd = p[1];
            }
        }
        return count;
    }
};

int main() {
    int n;
    cout << "Enter number of pairs: ";
    cin >> n;
    vector<vector<int>> pairs(n, vector<int>(2));
    for (int i = 0; i < n; i++) cin >> pairs[i][0] >> pairs[i][1];
    Solution sol;
    cout << "Maximum Chain Length: " << sol.findLongestChain(pairs) << endl;
}
```

---

### **Java**

```java
import java.util.*;

class Solution {
    public int findLongestChain(int[][] pairs) {
        Arrays.sort(pairs, (a, b) -> a[1] - b[1]);
        int count = 0, currEnd = Integer.MIN_VALUE;
        for (int[] p : pairs) {
            if (p[0] > currEnd) {
                count++;
                currEnd = p[1];
            }
        }
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of pairs: ");
        int n = sc.nextInt();
        int[][] pairs = new int[n][2];
        for (int i = 0; i < n; i++) {
            pairs[i][0] = sc.nextInt();
            pairs[i][1] = sc.nextInt();
        }
        Solution sol = new Solution();
        System.out.println("Maximum Chain Length: " + sol.findLongestChain(pairs));
    }
}
```

---

### **Python**

```python
class Solution:
    def findLongestChain(self, pairs):
        pairs.sort(key=lambda x: x[1])
        count, currEnd = 0, float("-inf")
        for a, b in pairs:
            if a > currEnd:
                count += 1
                currEnd = b
        return count

if __name__ == "__main__":
    n = int(input("Enter number of pairs: "))
    pairs = [list(map(int, input().split())) for _ in range(n)]
    sol = Solution()
    print("Maximum Chain Length:", sol.findLongestChain(pairs))
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    findLongestChain(pairs) {
        pairs.sort((a, b) => a[1] - b[1]);
        let count = 0, currEnd = -Infinity;
        for (let [a, b] of pairs) {
            if (a > currEnd) {
                count++;
                currEnd = b;
            }
        }
        return count;
    }
}

readline.question("Enter number of pairs: ", (nStr) => {
    const n = parseInt(nStr);
    const pairs = [];
    const rlInput = () => {
        if (pairs.length < n) {
            readline.question("", (line) => {
                pairs.push(line.split(" ").map(Number));
                rlInput();
            });
        } else {
            const sol = new Solution();
            console.log("Maximum Chain Length:", sol.findLongestChain(pairs));
            readline.close();
        }
    };
    rlInput();
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