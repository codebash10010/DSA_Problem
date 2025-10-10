
#  3Sum  - (LeetCode :- 15)

## 🏢 Companies Asked :- DoorDash✯, TikTok✯, Facebook✯, Amazon✯, Adobe✯, Google, Goldman Sachs, Microsoft, Apple, DE Shaw, Bloomberg

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium  

[🔗 Problem Link](https://leetcode.com/problems/3sum/description/)

---


## 🧩 Problem Statement
Given an integer array `nums`, return *all the unique triplets* `[nums[i], nums[j], nums[k]]` such that:

```

i != j, i != k, and j != k
nums[i] + nums[j] + nums[k] == 0

````

Notice that the solution set must **not contain duplicate triplets**.

### Example
**Input:**  
nums = [-1, 0, 1, 2, -1, -4]  
**Output:**  
[[-1, -1, 2], [-1, 0, 1]]

---

## 💡 Intuition
We want triplets that sum to zero.  
A brute-force solution would check all combinations (O(n³)),  
but we can do better using **sorting + two pointers**.

---

## ⚙️ Approach (Optimized - O(n²))
1. Sort the array.  
2. Loop through each element `i`:
   - Skip duplicate elements.
   - Use **two pointers**, `left` (i+1) and `right` (n-1).
   - If `nums[i] + nums[left] + nums[right] == 0`, store the triplet.
   - Adjust pointers while skipping duplicates.

---

## 🧠 Dry Run Example

Input: `nums = [-1, 0, 1, 2, -1, -4]`  
Sorted: `[-4, -1, -1, 0, 1, 2]`

| i | nums[i] | left | right | sum | Action |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | -4 | 1 | 5 | -3 | left++ |
| 1 | -1 | 2 | 5 | 0 | store [-1, -1, 2] |
| 1 | -1 | 3 | 4 | 0 | store [-1, 0, 1] |
| 2 | -1 | skip duplicate |   |   |   |

Final result: `[[-1, -1, 2], [-1, 0, 1]]`

---

## 🧩 Code Implementations

---

### 🧱 C++ Solution (with User Input)
```cpp
#include <bits/stdc++.h>
using namespace std;

vector<vector<int>> threeSum(vector<int>& nums) {
    vector<vector<int>> res;
    sort(nums.begin(), nums.end());
    int n = nums.size();

    for (int i = 0; i < n - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue;
        int left = i + 1, right = n - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                res.push_back({nums[i], nums[left], nums[right]});
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++; right--;
            } else if (sum < 0) left++;
            else right--;
        }
    }
    return res;
}

int main() {
    int n;
    cout << "Enter size of array: ";
    cin >> n;
    vector<int> nums(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> nums[i];

    vector<vector<int>> result = threeSum(nums);
    cout << "Triplets that sum to 0:\n";
    for (auto &v : result) {
        cout << "[";
        for (int i = 0; i < v.size(); i++) {
            cout << v[i] << (i < v.size() - 1 ? ", " : "");
        }
        cout << "]\n";
    }
}
````

---

### ☕ Java Solution (with User Input)

```java
import java.util.*;

public class Main {
    public static List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> res = new ArrayList<>();
        int n = nums.length;
        
        for (int i = 0; i < n - 2; i++) {
            if (i > 0 && nums[i] == nums[i - 1]) continue;
            int left = i + 1, right = n - 1;
            
            while (left < right) {
                int sum = nums[i] + nums[left] + nums[right];
                if (sum == 0) {
                    res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    while (left < right && nums[left] == nums[left + 1]) left++;
                    while (left < right && nums[right] == nums[right - 1]) right--;
                    left++; right--;
                } else if (sum < 0) left++;
                else right--;
            }
        }
        return res;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = sc.nextInt();
        int[] nums = new int[n];
        System.out.print("Enter elements: ");
        for (int i = 0; i < n; i++) nums[i] = sc.nextInt();
        
        List<List<Integer>> ans = threeSum(nums);
        System.out.println("Triplets that sum to 0:");
        for (List<Integer> triplet : ans)
            System.out.println(triplet);
    }
}
```

---

### 🐍 Python Solution (with User Input)

```python
def threeSum(nums):
    res = []
    nums.sort()
    n = len(nums)
    for i in range(n - 2):
        if i > 0 and nums[i] == nums[i - 1]:
            continue
        l, r = i + 1, n - 1
        while l < r:
            total = nums[i] + nums[l] + nums[r]
            if total == 0:
                res.append([nums[i], nums[l], nums[r]])
                while l < r and nums[l] == nums[l + 1]:
                    l += 1
                while l < r and nums[r] == nums[r - 1]:
                    r -= 1
                l += 1
                r -= 1
            elif total < 0:
                l += 1
            else:
                r -= 1
    return res

if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    nums = list(map(int, input("Enter elements: ").split()))
    print("Triplets that sum to 0:")
    print(threeSum(nums))
```

---

### ⚡ JavaScript Solution (with User Input)

```javascript
function threeSum(nums) {
  nums.sort((a, b) => a - b);
  const res = [];

  for (let i = 0; i < nums.length - 2; i++) {
    if (i > 0 && nums[i] === nums[i - 1]) continue;
    let left = i + 1,
      right = nums.length - 1;

    while (left < right) {
      const sum = nums[i] + nums[left] + nums[right];
      if (sum === 0) {
        res.push([nums[i], nums[left], nums[right]]);
        while (left < right && nums[left] === nums[left + 1]) left++;
        while (left < right && nums[right] === nums[right - 1]) right--;
        left++;
        right--;
      } else if (sum < 0) left++;
      else right--;
    }
  }
  return res;
}

const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter size of array: ", (n) => {
  readline.question("Enter elements: ", (line) => {
    const nums = line.split(" ").map(Number);
    console.log("Triplets that sum to 0:");
    console.log(threeSum(nums));
    readline.close();
  });
});
```

---

## 🧪 Sample Run

**Input**

```
6
-1 0 1 2 -1 -4
```

**Output**

```
Triplets that sum to 0:
[-1, -1, 2]
[-1, 0, 1]
```

---

## 🕒 Complexity

* **Time:** O(n²)
* **Space:** O(1) (excluding result storage)

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
