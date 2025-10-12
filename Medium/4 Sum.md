#  4Sum — (LeetCode - 18)

---

## Difficulty: 🟠 Medium

## 🏢 Companies Asked :- Microsoft 

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium 

---

👉 [Problem Link](https://leetcode.com/problems/4sum/)

---

## 📝 Problem Statement

Given an array `nums` of `n` integers, return **all the unique quadruplets** `[nums[a], nums[b], nums[c], nums[d]]` such that:

```

0 <= a, b, c, d < n
a, b, c, and d are distinct
nums[a] + nums[b] + nums[c] + nums[d] == target

```

You may return the answer **in any order**.

---

## 📌 Constraints

- `1 <= nums.length <= 200`
- `-10⁹ <= nums[i] <= 10⁹`
- `-10⁹ <= target <= 10⁹`

---

## 📌 Examples

### Example 1

**Input:**  
`nums = [1,0,-1,0,-2,2]`, `target = 0`

**Output:**  
`[[-2,-1,1,2], [-2,0,0,2], [-1,0,0,1]]`

**Explanation:**  
All unique quadruplets that sum to 0 are listed.

---

### Example 2

**Input:**  
`nums = [2,2,2,2,2]`, `target = 8`

**Output:**  
`[[2,2,2,2]]`

**Explanation:**  
Only one unique quadruplet possible.

---

## 💡 Intuition Behind the Approach

- This is an **extension of the 2Sum and 3Sum problems**.
- First, sort the array to simplify duplicate handling and two-pointer logic.
- Then fix two numbers (`i` and `j`) using nested loops.
- Use **two pointers** (`left` and `right`) for the remaining two numbers.
- Move the pointers intelligently based on the current sum compared to the target.
- Avoid duplicates at every step.

✅ Sorting helps manage duplicates easily.  
✅ Two-pointer approach reduces complexity from O(n⁴) to O(n³).

---

## 📚 Algorithm Steps

1. Sort the array `nums`.
2. Use two nested loops for the first two numbers: `i` and `j`.
3. Initialize two pointers:  
   - `left = j + 1`,  
   - `right = n - 1`.
4. Compute sum = `nums[i] + nums[j] + nums[left] + nums[right]`.
5. If sum == target → store quadruplet and move both pointers (skip duplicates).  
   If sum < target → move `left++`.  
   If sum > target → move `right--`.
6. Continue until all combinations are checked.

---

## 📊 Diagram

```

Example: nums = [1,0,-1,0,-2,2], target = 0
After sorting → [-2, -1, 0, 0, 1, 2]

Fix i = -2, j = -1 → need two numbers to sum 3
→ left=0, right=5
-2 + (-1) + 0 + 2 = -1 → move left++
-2 + (-1) + 1 + 2 = 0 ✅ Found [-2, -1, 1, 2]
Continue...

````

---

## 💻 Implementations (with User Input)

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> fourSum(vector<int>& nums, int target) {
    vector<vector<int>> res;
    sort(nums.begin(), nums.end());
    int n = nums.size();

    for (int i = 0; i < n - 3; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        for (int j = i + 1; j < n - 2; j++) {
            if (j > i + 1 && nums[j] == nums[j - 1]) continue;

            int left = j + 1, right = n - 1;
            while (left < right) {
                long long sum = (long long)nums[i] + nums[j] + nums[left] + nums[right];
                if (sum == target) {
                    res.push_back({nums[i], nums[j], nums[left], nums[right]});
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++; right--;
                } else if (sum < target) left++;
                else right--;
            }
        }
    }
    return res;
}

int main() {
    int n, target;
    cout << "Enter number of elements: ";
    cin >> n;
    vector<int> nums(n);
    cout << "Enter array elements: ";
    for (int i = 0; i < n; i++) cin >> nums[i];
    cout << "Enter target: ";
    cin >> target;

    vector<vector<int>> ans = fourSum(nums, target);
    cout << "Quadruplets:\n";
    for (auto& q : ans) {
        for (int x : q) cout << x << " ";
        cout << endl;
    }
}
````

---

### **Java**

```java
import java.util.*;

public class Main {
    public static List<List<Integer>> fourSum(int[] nums, int target) {
        List<List<Integer>> res = new ArrayList<>();
        Arrays.sort(nums);
        int n = nums.length;

        for (int i = 0; i < n - 3; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            for (int j = i + 1; j < n - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j - 1]) continue;

                int left = j + 1, right = n - 1;
                while (left < right) {
                    long sum = (long)nums[i] + nums[j] + nums[left] + nums[right];
                    if (sum == target) {
                        res.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
                        while (left < right && nums[left] == nums[left + 1]) left++;
                        while (left < right && nums[right] == nums[right - 1]) right--;
                        left++; right--;
                    } else if (sum < target) left++;
                    else right--;
                }
            }
        }
        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.print("Enter elements: ");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        System.out.print("Enter target: ");
        int target = sc.nextInt();

        List<List<Integer>> ans = fourSum(nums, target);
        System.out.println("Quadruplets:");
        for (List<Integer> q : ans) System.out.println(q);
    }
}
```

---

### **Python**

```python
def fourSum(nums, target):
    nums.sort()
    res = []
    n = len(nums)
    for i in range(n - 3):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        for j in range(i + 1, n - 2):
            if j > i + 1 and nums[j] == nums[j - 1]:
                continue
            left, right = j + 1, n - 1
            while left < right:
                total = nums[i] + nums[j] + nums[left] + nums[right]
                if total == target:
                    res.append([nums[i], nums[j], nums[left], nums[right]])
                    left += 1
                    right -= 1
                    while left < right and nums[left] == nums[left - 1]:
                        left += 1
                    while left < right and nums[right] == nums[right + 1]:
                        right -= 1
                elif total < target:
                    left += 1
                else:
                    right -= 1
    return res


if __name__ == "__main__":
    nums = list(map(int, input("Enter array elements: ").split()))
    target = int(input("Enter target: "))
    print("Quadruplets:", fourSum(nums, target))
```

---

### **JavaScript (Node.js)**

```javascript
function fourSum(nums, target) {
  nums.sort((a, b) => a - b);
  const res = [];
  const n = nums.length;

  for (let i = 0; i < n - 3; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    for (let j = i + 1; j < n - 2; j++) {
      if (j > i + 1 && nums[j] === nums[j - 1]) continue;

      let left = j + 1,
        right = n - 1;
      while (left < right) {
        const sum = nums[i] + nums[j] + nums[left] + nums[right];
        if (sum === target) {
          res.push([nums[i], nums[j], nums[left], nums[right]]);
          while (left < right && nums[left] === nums[left + 1]) left++;
          while (left < right && nums[right] === nums[right - 1]) right--;
          left++;
          right--;
        } else if (sum < target) left++;
        else right--;
      }
    }
  }
  return res;
}

// User input (Node.js)
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter array elements (space-separated): ", (arr) => {
  readline.question("Enter target: ", (t) => {
    const nums = arr.split(" ").map(Number);
    const target = parseInt(t);
    console.log("Quadruplets:", fourSum(nums, target));
    readline.close();
  });
});
```

---

## 🧪 Example Test Case

**Input:**
nums = `[1, 0, -1, 0, -2, 2]`, target = 0

**Output:**
`[[-2, -1, 1, 2], [-2, 0, 0, 2], [-1, 0, 0, 1]]`

---

## ⏱ Complexity

* Time Complexity: **O(n³)**
* Space Complexity: **O(1)** (excluding output)

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

