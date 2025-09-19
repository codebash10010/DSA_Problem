# Find in Mountain Array - (LeetCode :- 1095)

## Difficulty: 🔴 Hard

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:
👉 [https://leetcode.com/problems/find-in-mountain-array/](https://leetcode.com/problems/find-in-mountain-array/)

---

## 📝 Problem Statement

We define a **mountain array** as:

- `arr.length >= 3`
- There exists an index `i` such that:

  - `arr[0] < arr[1] < ... < arr[i]` (strictly increasing)
  - `arr[i] > arr[i+1] > ... > arr[n-1]` (strictly decreasing)

You are given a **MountainArray** interface (not direct access):

- `MountainArray.get(k)` → returns element at index `k`.
- `MountainArray.length()` → returns length.

Your task:
Return the **minimum index** such that `mountainArr.get(index) == target`.
If not found, return `-1`.

⚠️ Constraint: **You can make at most 100 calls to MountainArray.get**.

---

## 📌 Constraints

- `3 <= mountainArr.length() <= 10⁴`
- `0 <= target <= 10⁹`
- `0 <= mountainArr.get(i) <= 10⁹`

---

## 📌 Examples

### Example 1

**Input:**
mountainArr = \[1,2,3,4,5,3,1], target = 3

**Output:**
2

**Explanation:**
The target `3` appears at indices `[2,5]`.
Return **minimum index = 2**.

---

### Example 2

**Input:**
mountainArr = \[0,1,2,4,2,1], target = 3

**Output:**
-1

**Explanation:**
Target does not exist in array → return `-1`.

---

## 💡 Intuition Behind the Approach

This problem is **Binary Search on Mountain Array** 🔥

Steps:

1. **Find Peak Index**

   - Use binary search to locate the peak (maximum element).

2. **Binary Search on Increasing Part**

   - Perform binary search (`O(log n)`) on `[0 … peak]`.

3. **Binary Search on Decreasing Part**

   - Perform binary search (`O(log n)`) on `[peak … n-1]`, but reversed.

4. **Return earliest index if found**, else `-1`.

✅ This ensures **O(log n)** time complexity with minimal API calls.

---

## 📚 Algorithm Explanation

- Binary search to find peak (`arr[mid] < arr[mid+1]` → move right, else left).
- Binary search in **left half (increasing)**.
- If not found, binary search in **right half (decreasing)**.
- Return result.

---

## 💻 Implementations

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

// Simulating MountainArray for user input
class MountainArray {
    vector<int> arr;
public:
    MountainArray(vector<int> a) : arr(a) {}
    int get(int index) { return arr[index]; }
    int length() { return arr.size(); }
};

class Solution {
public:
    int findInMountainArray(int target, MountainArray &mountainArr) {
        int n = mountainArr.length();

        // 1. Find peak
        int l = 0, r = n - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (mountainArr.get(mid) < mountainArr.get(mid + 1)) l = mid + 1;
            else r = mid;
        }
        int peak = l;

        // 2. Binary search left side
        int ans = binarySearch(mountainArr, target, 0, peak, true);
        if (ans != -1) return ans;

        // 3. Binary search right side
        return binarySearch(mountainArr, target, peak + 1, n - 1, false);
    }

private:
    int binarySearch(MountainArray &mountainArr, int target, int l, int r, bool asc) {
        while (l <= r) {
            int mid = (l + r) / 2;
            int val = mountainArr.get(mid);
            if (val == target) return mid;
            if (asc) {
                if (val < target) l = mid + 1;
                else r = mid - 1;
            } else {
                if (val > target) l = mid + 1;
                else r = mid - 1;
            }
        }
        return -1;
    }
};

// Driver
int main() {
    int n, target;
    cout << "Enter size of array: ";
    cin >> n;
    vector<int> arr(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> arr[i];
    cout << "Enter target: ";
    cin >> target;

    MountainArray mountainArr(arr);
    Solution sol;
    cout << "Index: " << sol.findInMountainArray(target, mountainArr) << endl;
}
```

---

### **Java**

```java
import java.util.*;

class MountainArray {
    private int[] arr;
    MountainArray(int[] a) { arr = a; }
    public int get(int index) { return arr[index]; }
    public int length() { return arr.length; }
}

class Solution {
    public int findInMountainArray(int target, MountainArray mountainArr) {
        int n = mountainArr.length();

        // 1. Find peak
        int l = 0, r = n - 1;
        while (l < r) {
            int mid = (l + r) / 2;
            if (mountainArr.get(mid) < mountainArr.get(mid + 1)) l = mid + 1;
            else r = mid;
        }
        int peak = l;

        // 2. Search left
        int ans = binarySearch(mountainArr, target, 0, peak, true);
        if (ans != -1) return ans;

        // 3. Search right
        return binarySearch(mountainArr, target, peak + 1, n - 1, false);
    }

    private int binarySearch(MountainArray mountainArr, int target, int l, int r, boolean asc) {
        while (l <= r) {
            int mid = (l + r) / 2;
            int val = mountainArr.get(mid);
            if (val == target) return mid;
            if (asc) {
                if (val < target) l = mid + 1;
                else r = mid - 1;
            } else {
                if (val > target) l = mid + 1;
                else r = mid - 1;
            }
        }
        return -1;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.println("Enter elements: ");
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
        System.out.print("Enter target: ");
        int target = sc.nextInt();

        MountainArray mountainArr = new MountainArray(arr);
        Solution sol = new Solution();
        System.out.println("Index: " + sol.findInMountainArray(target, mountainArr));
    }
}
```

---

### **Python**

```python
class MountainArray:
    def __init__(self, arr):
        self.arr = arr
    def get(self, index):
        return self.arr[index]
    def length(self):
        return len(self.arr)

class Solution:
    def findInMountainArray(self, target, mountainArr):
        n = mountainArr.length()

        # 1. Find peak
        l, r = 0, n - 1
        while l < r:
            mid = (l + r) // 2
            if mountainArr.get(mid) < mountainArr.get(mid + 1):
                l = mid + 1
            else:
                r = mid
        peak = l

        # 2. Binary search left
        ans = self.binarySearch(mountainArr, target, 0, peak, True)
        if ans != -1: return ans

        # 3. Binary search right
        return self.binarySearch(mountainArr, target, peak+1, n-1, False)

    def binarySearch(self, mountainArr, target, l, r, asc):
        while l <= r:
            mid = (l + r) // 2
            val = mountainArr.get(mid)
            if val == target: return mid
            if asc:
                if val < target: l = mid + 1
                else: r = mid - 1
            else:
                if val > target: l = mid + 1
                else: r = mid - 1
        return -1

# Driver
if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    arr = list(map(int, input("Enter elements: ").split()))
    target = int(input("Enter target: "))
    mountainArr = MountainArray(arr)
    sol = Solution()
    print("Index:", sol.findInMountainArray(target, mountainArr))
```

---

### **JavaScript**

```javascript
class MountainArray {
  constructor(arr) {
    this.arr = arr;
  }
  get(index) {
    return this.arr[index];
  }
  length() {
    return this.arr.length;
  }
}

class Solution {
  findInMountainArray(target, mountainArr) {
    const n = mountainArr.length();

    // 1. Find peak
    let l = 0,
      r = n - 1;
    while (l < r) {
      let mid = Math.floor((l + r) / 2);
      if (mountainArr.get(mid) < mountainArr.get(mid + 1)) l = mid + 1;
      else r = mid;
    }
    let peak = l;

    // 2. Search left
    let ans = this.binarySearch(mountainArr, target, 0, peak, true);
    if (ans !== -1) return ans;

    // 3. Search right
    return this.binarySearch(mountainArr, target, peak + 1, n - 1, false);
  }

  binarySearch(mountainArr, target, l, r, asc) {
    while (l <= r) {
      let mid = Math.floor((l + r) / 2);
      let val = mountainArr.get(mid);
      if (val === target) return mid;
      if (asc) {
        if (val < target) l = mid + 1;
        else r = mid - 1;
      } else {
        if (val > target) l = mid + 1;
        else r = mid - 1;
      }
    }
    return -1;
  }
}

// Driver
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter size of array: ", (nStr) => {
  readline.question("Enter elements: ", (arrStr) => {
    let arr = arrStr.trim().split(" ").map(Number);
    readline.question("Enter target: ", (tStr) => {
      let target = parseInt(tStr);
      let mountainArr = new MountainArray(arr);
      let sol = new Solution();
      console.log("Index:", sol.findInMountainArray(target, mountainArr));
      readline.close();
    });
  });
});
```

---

## 🧪 Tests You Can Try

**Input 1:**
arr = \[1,2,3,4,5,3,1], target = 3
**Output:**
2

**Input 2:**
arr = \[0,1,2,4,2,1], target = 3
**Output:**
-1

**Input 3:**
arr = \[1,5,2], target = 2
**Output:**
2

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
