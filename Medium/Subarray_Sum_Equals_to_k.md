# Subarray Sum Equals K - (LeetCode :- 560)

## Difficulty: 🟠 Medium

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given an array of integers `nums` and an integer `k`, return the **total number of subarrays** whose sum equals to `k`. A subarray is a **contiguous non-empty** sequence of elements inside the array.
You must count all such subarrays.

---

## 📌 Constraints

- `1 <= nums.length <= 2 * 10^4`
- `-1000 <= nums[i] <= 1000`
- `-10^7 <= k <= 10^7`

---

## 📌 Examples

### Example 1

**Input:**
nums = \[1,1,1], k = 2
**Output:**
2
**Explanation:**
Subarrays are \[1,1] (from index 0 to 1) and \[1,1] (from index 1 to 2).

---

### Example 2

**Input:**
nums = \[1,2,3], k = 3
**Output:**
2
**Explanation:**
Subarrays: \[1,2] and \[3].

---

### Example 3

**Input:**
nums = \[2,-1,2,1], k = 3
**Output:**
3
**Explanation:**
Subarrays: \[2, -1, 2], \[2, -1, 2, 1] (if sum =3), also \[1,2] etc. (depending on indices).

---

## 💡 Intuition Behind the Approach

A naive approach would check all possible subarrays (nested loops) and sum them — O(n²) time in worst case. But with prefix sums + a hash map (or dictionary), we can do it in O(n) time:

- Keep a running sum as you traverse the array.
- Use a hash map to store how many times each prefix sum has occurred so far.
- For each position `i`, when the running sum is `currSum`, see if `currSum - k` has occurred before — that means there is a subarray ending at `i` whose sum is `k`.
- Also, check if `currSum` itself equals `k` (subarray from start).

This gives O(n) time, O(n) space.

---

## 📚 Algorithm Explanation

1. Initialize `count = 0`, `runningSum = 0`.
2. Hash map `prefixCount` with default `{0:1}` (to account for subarrays starting at index 0).
3. Loop over each element `num` in `nums`:

   - `runningSum += num`
   - If `(runningSum - k)` exists in `prefixCount`, add its frequency to `count`.
   - Increment `prefixCount[runningSum]`.

4. Return `count`.

---

## 💻 Implementations (with user input)

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int subarraySum(vector<int>& nums, int k) {
        unordered_map<long long, int> prefixCount;
        prefixCount[0] = 1;
        long long runningSum = 0;
        int count = 0;
        for (int num : nums) {
            runningSum += num;
            long long need = runningSum - k;
            if (prefixCount.find(need) != prefixCount.end())
                count += prefixCount[need];
            prefixCount[runningSum]++;
        }
        return count;
    }
};

int main() {
    int n, k;
    cout << "Enter size of array: ";
    cin >> n;
    vector<int> nums(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> nums[i];
    cout << "Enter k: ";
    cin >> k;

    Solution sol;
    int result = sol.subarraySum(nums, k);
    cout << "Number of subarrays summing to " << k << " = " << result << endl;

    return 0;
}
```

---

### **Java**

```java
import java.util.*;

class Solution {
    public int subarraySum(int[] nums, int k) {
        Map<Long, Integer> prefixCount = new HashMap<>();
        prefixCount.put(0L, 1);
        long runningSum = 0;
        int count = 0;
        for (int num : nums) {
            runningSum += num;
            long need = runningSum - k;
            if (prefixCount.containsKey(need)) {
                count += prefixCount.get(need);
            }
            prefixCount.put(runningSum, prefixCount.getOrDefault(runningSum, 0) + 1);
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        System.out.print("Enter k: ");
        int k = sc.nextInt();

        Solution sol = new Solution();
        int result = sol.subarraySum(nums, k);
        System.out.println("Number of subarrays summing to " + k + " = " + result);
    }
}
```

---

### **Python**

```python
class Solution:
    def subarraySum(self, nums, k):
        prefix_count = {0: 1}
        running_sum = 0
        count = 0
        for num in nums:
            running_sum += num
            need = running_sum - k
            if need in prefix_count:
                count += prefix_count[need]
            prefix_count[running_sum] = prefix_count.get(running_sum, 0) + 1
        return count

if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    nums = list(map(int, input("Enter elements: ").split()))
    k = int(input("Enter k: "))
    sol = Solution()
    result = sol.subarraySum(nums, k)
    print("Number of subarrays summing to", k, "=", result)
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

class Solution {
  subarraySum(nums, k) {
    const prefixCount = new Map();
    prefixCount.set(0, 1);
    let runningSum = 0;
    let count = 0;
    for (const num of nums) {
      runningSum += num;
      const need = runningSum - k;
      if (prefixCount.has(need)) {
        count += prefixCount.get(need);
      }
      prefixCount.set(runningSum, (prefixCount.get(runningSum) || 0) + 1);
    }
    return count;
  }
}

readline.question("Enter size of array: ", (nStr) => {
  readline.question("Enter elements (space-separated): ", (arrStr) => {
    const nums = arrStr.trim().split(" ").map(Number);
    readline.question("Enter k: ", (kStr) => {
      const k = Number(kStr);
      const sol = new Solution();
      const result = sol.subarraySum(nums, k);
      console.log(`Number of subarrays summing to ${k} = ${result}`);
      readline.close();
    });
  });
});
```

---

## 🧪 Tests You Can Try

Input:
nums = \[1,1,1]
k = 2
Output: 2

Input:
nums = \[1,2,3]
k = 3
Output: 2

Input:
nums = \[2,-1,2,1]
k = 3
Output: 3

Input:
nums = \[3,4,7,2,-3,1,4,2]
k = 7
Output: 4

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
