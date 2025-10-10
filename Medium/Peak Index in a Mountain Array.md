# Peak Index in a Mountain Array - (LeetCode :- 852)

## 🏢 Companies Asked :- Josh

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

**Difficulty:** 🟠 Medium  

[🔗 Problem Link] (https://leetcode.com/problems/peak-index-in-a-mountain-array/)

---

## 📝 Problem Statement

You are given an integer array `arr` that is a **mountain array**. That means:

* `arr.length >= 3`,
* There exists some index `i` with `0 < i < arr.length - 1` such that:

  * `arr[0] < arr[1] < … < arr[i - 1] < arr[i]`
  * `arr[i] > arr[i + 1] > … > arr[arr.length - 1]`

Return the **index `i`** where this peak occurs (i.e. `arr[i]` is strictly greater than its neighbors).

---

## 📌 Constraints

* `3 <= arr.length <= 10^5`
* `0 <= arr[i] <= 10^6`
* It is guaranteed `arr` is a valid mountain array.

---

## 📌 Examples

### **Example 1**

**Input:**
arr = [0,2,1,0]

**Output:**
1

**Explanation:**
The peak element is `2` at index `1`.

---

### **Example 2**

**Input:**
arr = [0,10,5,2]

**Output:**
1

---

### **Example 3**

**Input:**
arr = [3,4,5,1]

**Output:**
2

---

## 💡 Intuition Behind the Approach

Since the array **first increases then decreases**, we can use **Binary Search** to find the peak:

* If `arr[mid] > arr[mid+1]`, you are in the descending slope → move `right = mid`.
* Otherwise, you are in the ascending slope → move `left = mid + 1`.

Finally, `left == right` will give the peak index.

---

## 📚 Algorithm Explanation

1. Initialize: `left = 1`, `right = n - 2`
2. While `left < right`:

   * Compute mid.
   * If `arr[mid] > arr[mid+1]` → peak is at `mid` or left side.
   * Else → peak is at right side.
3. Return `left`.

**Time Complexity:** `O(log n)`
**Space Complexity:** `O(1)`

---

## 💻 Implementations

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    int peakIndexInMountainArray(vector<int>& arr) {
        int left = 1, right = arr.size() - 2;
        while (left < right) {
            int mid = (left + right) / 2;
            if (arr[mid] > arr[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
};

int main() {
    int n;
    cout << "Enter size of array: ";
    cin >> n;
    vector<int> arr(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> arr[i];
    Solution sol;
    cout << "Peak Index: " << sol.peakIndexInMountainArray(arr) << endl;
}
```

---

### **Java**

```java
import java.util.*;

class Solution {
    public int peakIndexInMountainArray(int[] arr) {
        int left = 1, right = arr.length - 2;
        while (left < right) {
            int mid = (left + right) / 2;
            if (arr[mid] > arr[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter size of array: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.print("Enter elements: ");
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
        Solution sol = new Solution();
        System.out.println("Peak Index: " + sol.peakIndexInMountainArray(arr));
    }
}
```

---

### **Python**

```python
class Solution:
    def peakIndexInMountainArray(self, arr):
        left, right = 1, len(arr) - 2
        while left < right:
            mid = (left + right) // 2
            if arr[mid] > arr[mid + 1]:
                right = mid
            else:
                left = mid + 1
        return left

if __name__ == "__main__":
    n = int(input("Enter size of array: "))
    arr = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    print("Peak Index:", sol.peakIndexInMountainArray(arr))
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    peakIndexInMountainArray(arr) {
        let left = 1, right = arr.length - 2;
        while (left < right) {
            let mid = Math.floor((left + right) / 2);
            if (arr[mid] > arr[mid + 1]) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        return left;
    }
}

readline.question("Enter size of array: ", (nStr) => {
    const n = parseInt(nStr);
    readline.question("Enter elements: ", (arrStr) => {
        const arr = arrStr.split(" ").map(Number);
        const sol = new Solution();
        console.log("Peak Index:", sol.peakIndexInMountainArray(arr));
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

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---
