# Concatenation of Array - (LeetCode :- 1929)

## Difficulty: 🟢 Easy

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:
👉 [https://leetcode.com/problems/concatenation-of-array/description/](https://leetcode.com/problems/concatenation-of-array/description/) ([LeetCode][1])

---

## 📝 Problem Statement

Given an integer array `nums` of length `n`, return an array `ans` of length `2n` where:

- The first `n` elements of `ans` are the same as `nums`: `ans[i] == nums[i]` for `0 <= i < n`
- The next `n` elements of `ans` are again the same as `nums`: `ans[i + n] == nums[i]` for `0 <= i < n`

In other words, you need to concatenate the array `nums` with itself.

---

## 📌 Constraints

- `n == nums.length`
- `1 <= n <= 1000`
- `1 <= nums[i] <= 1000`

---

## 📌 Examples

### Example 1

**Input:**
nums = \[1,2,1]

**Output:**
\[1,2,1,1,2,1]

---

### Example 2

**Input:**
nums = \[1,3,2,1]

**Output:**
\[1,3,2,1,1,3,2,1]

---

## 💡 Intuition Behind the Approach

The problem is very simple: just repeat the array twice, one after the other.

- Either build a new array (`ans`) of size `2n` and fill the first half with `nums`, then fill the second half also with `nums`.
- Or take advantage of language features (like concatenation) that allow you to join two lists/arrays.

Time complexity is `O(n)` since you process each element twice at most.
Space complexity is `O(n)` for the result.

---

## 📚 Algorithm Explanation

1. Read `n` (length of `nums`).
2. Read `nums` array.
3. Create an array `ans` of length `2n`.
4. Loop `i` from `0` to `n-1`:

   - `ans[i] = nums[i]`
   - `ans[i + n] = nums[i]`

5. Return `ans`.

---

## 💻 Implementations (with user input)

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<int> getConcatenation(const vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(2 * n);
        for (int i = 0; i < n; i++) {
            ans[i] = nums[i];
            ans[i + n] = nums[i];
        }
        return ans;
    }
};

int main() {
    int n;
    cout << "Enter size of array: ";
    cin >> n;
    vector<int> nums(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> nums[i];

    Solution sol;
    vector<int> res = sol.getConcatenation(nums);

    cout << "Concatenated array: ";
    for (int x : res) cout << x << " ";
    cout << endl;

    return 0;
}
```

---

### **Java**

```java
import java.util.*;

class Solution {
    public int[] getConcatenation(int[] nums) {
        int n = nums.length;
        int[] ans = new int[2 * n];
        for (int i = 0; i < n; i++) {
            ans[i] = nums[i];
            ans[i + n] = nums[i];
        }
        return ans;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();

        Solution sol = new Solution();
        int[] res = sol.getConcatenation(nums);

        System.out.print("Concatenated array: ");
        for (int x : res) System.out.print(x + " ");
        System.out.println();
    }
}
```

---

### **Python**

```python
class Solution:
    def getConcatenation(self, nums: list[int]) -> list[int]:
        n = len(nums)
        ans = [0] * (2 * n)
        for i in range(n):
            ans[i] = nums[i]
            ans[i + n] = nums[i]
        return ans

if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    nums = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    res = sol.getConcatenation(nums)
    print("Concatenated array:", *res)
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

class Solution {
  getConcatenation(nums) {
    const n = nums.length;
    const ans = new Array(2 * n);
    for (let i = 0; i < n; i++) {
      ans[i] = nums[i];
      ans[i + n] = nums[i];
    }
    return ans;
  }
}

readline.question("Enter size of array: ", (nStr) => {
  readline.question("Enter elements (space-separated): ", (arrStr) => {
    const nums = arrStr.trim().split(" ").map(Number);
    const sol = new Solution();
    const res = sol.getConcatenation(nums);
    console.log("Concatenated array:", res.join(" "));
    readline.close();
  });
});
```

---

## 🧪 Tests You Can Try

Input:
nums = \[1,2,1]
Output: \[1,2,1,1,2,1]

Input:
nums = \[1,3,2,1]
Output: \[1,3,2,1,1,3,2,1]

Input:
nums = \[4]
Output: \[4,4]

Input:
nums = \[5,6,7,8]
Output: \[5,6,7,8,5,6,7,8]

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

### **JavaScript (Node.js)**

```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---
