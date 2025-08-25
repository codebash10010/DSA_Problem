# Next Greater Element II - (LeetCode :- 503)

## 🏢 Companies Asked :- DoorDash✯, TikTok✯, Facebook✯, Amazon✯, Adobe✯, Google, Goldman Sachs, Microsoft, Apple, DE Shaw, Bloomberg

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/next-greater-element-i/

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/next-greater-element-ii/

---

## 📝 Problem Statement

You are given a **circular integer array** `nums` (i.e., the next element of `nums[nums.length - 1]` is `nums[0]`).  

Return the **next greater number** for every element in `nums`.  

- The next greater number of a number `x` is the **first greater number** to its traversing-order next in the array.  
- Since the array is **circular**, you may wrap around and continue searching.  
- If it doesn’t exist, return `-1` for that number.  

---

## 📌 Constraints
- `1 <= nums.length <= 10⁴`
- `-10⁹ <= nums[i] <= 10⁹`

---

## 📌 Examples

### **Example 1**
**Input:**  
nums = [1,2,1]

**Output:**  
[2, -1, 2]

**Explanation:**  
- First `1` → next greater is `2`.  
- `2` → no greater element found → `-1`.  
- Second `1` → needs circular lookup → next greater is `2`.

---

### **Example 2**
**Input:**  
nums = [1,2,3,4,3]

**Output:**  
[2, 3, 4, -1, 4]

---

## 💡 Intuition Behind the Approach

This problem is a **circular extension** of **Next Greater Element I**.

👉 Key idea:  
- Since the array is circular, every element should have a chance to look at **both its right side and left side**.  
- We can simulate this by traversing the array **twice** (2 * n length).  

👉 Steps:
1. Traverse the array from **right to left** (twice the length).  
2. Use a **monotonic stack** to keep potential "next greater" candidates.  
3. For each element:  
   - Pop smaller/equal elements (not useful).  
   - The top of the stack (if any) = **next greater**.  
   - Push current element to stack.  
4. Store results only for first `n` elements.  

🔑 This ensures circularity is respected without explicitly rotating.

---

## 📚 Algorithm Explanation

- Traverse `2 * n` times (from rightmost to left).  
- Maintain a **decreasing stack**.  
- Store answers for indices in the first `n`.  

**Time Complexity:** `O(n)` (each element is pushed/popped at most once)  
**Space Complexity:** `O(n)` (stack + output array)

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
#include <stack>
using namespace std;

class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int n = nums.size();
        vector<int> ans(n, -1);
        stack<int> st;
        
        for (int i = 2 * n - 1; i >= 0; i--) {
            int num = nums[i % n];
            while (!st.empty() && st.top() <= num) {
                st.pop();
            }
            if (i < n) {
                ans[i] = st.empty() ? -1 : st.top();
            }
            st.push(num);
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
    vector<int> ans = sol.nextGreaterElements(nums);
    
    cout << "Next Greater Elements: ";
    for (int x : ans) cout << x << " ";
    cout << endl;
}
```
---

### **Java**
```Java
import java.util.*;

class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int n = nums.length;
        int[] ans = new int[n];
        Arrays.fill(ans, -1);
        Stack<Integer> st = new Stack<>();
        
        for (int i = 2 * n - 1; i >= 0; i--) {
            int num = nums[i % n];
            while (!st.isEmpty() && st.peek() <= num) {
                st.pop();
            }
            if (i < n) {
                ans[i] = st.isEmpty() ? -1 : st.peek();
            }
            st.push(num);
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
        System.out.println("Enter elements: ");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        
        Solution sol = new Solution();
        int[] ans = sol.nextGreaterElements(nums);
        
        System.out.print("Next Greater Elements: ");
        for (int x : ans) System.out.print(x + " ");
    }
}


```
---

### **Pyhton**
```Pyhton
class Solution:
    def nextGreaterElements(self, nums):
        n = len(nums)
        ans = [-1] * n
        stack = []
        
        for i in range(2 * n - 1, -1, -1):
            num = nums[i % n]
            while stack and stack[-1] <= num:
                stack.pop()
            if i < n:
                ans[i] = stack[-1] if stack else -1
            stack.append(num)
        
        return ans

if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    nums = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    print("Next Greater Elements:", sol.nextGreaterElements(nums))

```
---

### **JavaScript**
```JavaScript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    nextGreaterElements(nums) {
        const n = nums.length;
        const ans = new Array(n).fill(-1);
        const stack = [];
        
        for (let i = 2 * n - 1; i >= 0; i--) {
            const num = nums[i % n];
            while (stack.length && stack[stack.length - 1] <= num) {
                stack.pop();
            }
            if (i < n) {
                ans[i] = stack.length ? stack[stack.length - 1] : -1;
            }
            stack.push(num);
        }
        return ans;
    }
}

readline.question("Enter size of array: ", (nStr) => {
    readline.question("Enter elements: ", (arrStr) => {
        const nums = arrStr.trim().split(" ").map(Number);
        const sol = new Solution();
        console.log("Next Greater Elements:", sol.nextGreaterElements(nums).join(" "));
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