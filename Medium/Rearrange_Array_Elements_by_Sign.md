# Rearrange Array Elements by Sign - (LeetCode :- 2149)

## 🏢 Companies Asked :- Amazon , Microsoft , Google , Bloomberg , Adobe  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/rearrange-array-elements-by-sign/

---


## 📝 Problem Statement

You are given a **0-indexed integer array `nums` of even length** consisting of an **equal number of positive and negative integers**.

You should return the array such that the following conditions are satisfied:

1. Every consecutive pair of integers have **opposite signs**.  
2. For all integers with the same sign, the **relative order** in which they appear in `nums` is preserved.  
3. The rearranged array begins with a **positive integer**.  

Return the modified array.

---

## 📌 Constraints
- `2 <= nums.length <= 2 * 10⁵`
- `nums.length` is **even**
- `1 <= |nums[i]| <= 10⁵`
- `nums` contains equal numbers of **positive** and **negative** integers.

---

## 📌 Examples

### **Example 1**
**Input:**

nums = [3,1,-2,-5,2,-4]

**Output:**

[3,-2,1,-5,2,-4]

**Explanation with diagram:**
Positives: [3, 1, 2]

Negatives: [-2, -5, -4]

Rearrange → [3, -2, 1, -5, 2, -4]

---

### **Example 2**

**Input:**

nums = [-1,1]

**Output:**

[1,-1]

**Explanation with diagram:**

Positives: [1]
Negatives: [-1]

Rearrange → [1, -1]


---



## 📚 Algorithm Explanation

We maintain **two pointers**:
- One iterating through positive numbers.  
- One iterating through negative numbers.  

Then, we construct the output array by alternately picking:
- A positive number → then a negative number → repeat…  

Since both positives and negatives are equal in count, this will always produce a valid result.

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(n)` (can’t be done in-place while preserving order).

---



## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    vector<int> rearrangeArray(vector<int>& nums) {
        vector<int> pos, neg;
        for (int num : nums) {
            if (num > 0) pos.push_back(num);
            else neg.push_back(num);
        }
        vector<int> ans;
        for (int i = 0; i < pos.size(); i++) {
            ans.push_back(pos[i]);
            ans.push_back(neg[i]);
        }
        return ans;
    }
};

int main() {
    int n;
    cout << "Enter number of elements: ";
    cin >> n;
    vector<int> nums(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> nums[i];

    Solution sol;
    vector<int> ans = sol.rearrangeArray(nums);

    cout << "Rearranged array: ";
    for (int x : ans) cout << x << " ";
    cout << endl;
}
```
---
### **Java**

```java

import java.util.*;

class Solution {
    public int[] rearrangeArray(int[] nums) {
        List<Integer> pos = new ArrayList<>(), neg = new ArrayList<>();
        for (int num : nums) {
            if (num > 0) pos.add(num);
            else neg.add(num);
        }
        int[] ans = new int[nums.length];
        int idx = 0;
        for (int i = 0; i < pos.size(); i++) {
            ans[idx++] = pos.get(i);
            ans[idx++] = neg.get(i);
        }
        return ans;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();

        Solution sol = new Solution();
        int[] ans = sol.rearrangeArray(nums);

        System.out.print("Rearranged array: ");
        for (int x : ans) System.out.print(x + " ");
        System.out.println();
    }
}
```

---
### **Python**

```Python

class Solution:
    def rearrangeArray(self, nums):
        pos = [x for x in nums if x > 0]
        neg = [x for x in nums if x < 0]
        ans = []
        for i in range(len(pos)):
            ans.append(pos[i])
            ans.append(neg[i])
        return ans

if __name__ == "__main__":
    n = int(input("Enter number of elements: "))
    nums = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    ans = sol.rearrangeArray(nums)
    print("Rearranged array:", *ans)

```
---

### **JavaScript**
```JavaScript


const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    rearrangeArray(nums) {
        const pos = nums.filter(x => x > 0);
        const neg = nums.filter(x => x < 0);
        const ans = [];
        for (let i = 0; i < pos.length; i++) {
            ans.push(pos[i]);
            ans.push(neg[i]);
        }
        return ans;
    }
}

readline.question("Enter number of elements: ", (nStr) => {
    readline.question("Enter elements (space-separated): ", (arrStr) => {
        const nums = arrStr.trim().split(" ").map(Number);
        const sol = new Solution();
        const ans = sol.rearrangeArray(nums);
        console.log("Rearranged array:", ans.join(" "));
        readline.close();
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

---



