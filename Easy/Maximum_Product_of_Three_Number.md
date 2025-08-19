# Maximum Product of Three Numbers - (LeetCode :- 628)

## 🏢 Companies Asked :- Amazon, Microsoft, Google, Facebook, Bloomberg, Adobe  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/maximum-product-of-three-numbers/

---

## 📝 Problem Statement

Given an integer array `nums`, find **three numbers** whose product is **maximum** and return that product.

---

## 📌 Constraints
- `3 <= nums.length <= 10⁴`
- `-1000 <= nums[i] <= 1000`

---

## 📌 Examples

### **Example 1**
**Input:**
nums = [1,2,3]

**Output:**
6

---

### **Example 2**
**Input:**
nums = [1,2,3,4]

**Output:**
24


---

### **Example 3**
**Input:**
nums = [-1,-2,-3]

**Output:**
-6




---

## 💡 Intuition Behind the Approach

The product of three numbers can be maximum in **two cases**:

1. **Top 3 largest positive numbers**  
   Example: `[1, 2, 3, 4]` → product is `2 * 3 * 4 = 24`

2. **Two smallest negative numbers + largest positive number**  
   Example: `[-10, -10, 5, 2]` → product is `-10 * -10 * 5 = 500`

👉 So, the **maximum product** is:
max( largest1 * largest2 * largest3 , smallest1 * smallest2 * largest1 )



🔑 **Key Idea:** Sort the array (or find min2 and max3 efficiently) and compute both options.

---

## 📚 Algorithm Explanation

1. **Sort the array.**
2. Extract:
   - `largest1, largest2, largest3` (three largest elements)
   - `smallest1, smallest2` (two smallest elements)
3. Compute:
   - Product1 = `largest1 * largest2 * largest3`
   - Product2 = `smallest1 * smallest2 * largest1`
4. Return `max(Product1, Product2)`

**Time Complexity:** `O(n log n)` (due to sorting)  
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
    int maximumProduct(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        int prod1 = nums[n-1] * nums[n-2] * nums[n-3];
        int prod2 = nums[0] * nums[1] * nums[n-1];
        return max(prod1, prod2);
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
    cout << "Maximum Product of Three Numbers: " << sol.maximumProduct(nums) << endl;
}
```
---
### **Java**

```java


import java.util.*;

class Solution {
    public int maximumProduct(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        int prod1 = nums[n-1] * nums[n-2] * nums[n-3];
        int prod2 = nums[0] * nums[1] * nums[n-1];
        return Math.max(prod1, prod2);
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
        System.out.println("Maximum Product of Three Numbers: " + sol.maximumProduct(nums));
    }
}


```

---
### **Python**

```Python
class Solution:
    def maximumProduct(self, nums):
        nums.sort()
        return max(nums[-1] * nums[-2] * nums[-3], nums[0] * nums[1] * nums[-1])

if __name__ == "__main__":
    n = int(input("Enter number of elements: "))
    nums = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    print("Maximum Product of Three Numbers:", sol.maximumProduct(nums))


```
---

### **JavaScript**
```JavaScript


const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    maximumProduct(nums) {
        nums.sort((a, b) => a - b);
        let n = nums.length;
        let prod1 = nums[n-1] * nums[n-2] * nums[n-3];
        let prod2 = nums[0] * nums[1] * nums[n-1];
        return Math.max(prod1, prod2);
    }
}

readline.question("Enter number of elements: ", (nStr) => {
    readline.question("Enter elements (space-separated): ", (arrStr) => {
        const nums = arrStr.trim().split(" ").map(Number);
        const sol = new Solution();
        console.log("Maximum Product of Three Numbers:", sol.maximumProduct(nums));
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
