# Duplicate Zeros - (LeetCode :- 1089)

## 🏢 Companies Asked :- Amazon , Microsoft ,Google , Adobe  , Facebook  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/duplicate-zeros/description/


---

## 📝 Problem Statement

Given a fixed-length integer array `arr`, **duplicate each occurrence of zero**, shifting the remaining elements to the right.

**Important:**
- Elements beyond the length of the original array are **not written**.
- Perform the modifications **in place** and **do not return anything**.

---

## 📌 Constraints
- `1 <= arr.length <= 10⁴`
- `0 <= arr[i] <= 9`

---

## 📌 Examples

### **Example 1**

Input: arr = [1,0,2,3,0,4,5,0]

Output: [1,0,0,2,3,0,0,4]

**Step-by-step diagram:**

Index: 0 1 2 3 4 5 6 7

Value: [1, 0, 2, 3, 0, 4, 5, 0]

**↓ duplicate**

After: [1, 0, 0, 2, 3, 0, 0, 4]

### **Example 2**

Input: arr = [1,2,3]
Output: [1,2,3]

**Step-by-step diagram:**

[1, 2, 3] → No zeros → No change



---


### Example Walkthrough

**Input:**  

[1, 0, 2, 3, 0, 4, 5, 0]


```

## Duplicate Zeros - Step-by-Step Execution (Forward Order)

**Initial Array:**  
[1, 0, 2, 3, 0, 4, 5, 0]  
**Count of zeros:** 3  

---

| Step | i  | j  | Action                          | Array after step               |
|------|----|----|---------------------------------|---------------------------------|
| 1    | 0  | 0  | Copy 1                         | [1, _, _, _, _, _, _, _]        |
| 2    | 1  | 1  | Zero → duplicate if space      | [1, 0, 0, _, _, _, _, _]        |
| 3    | 2  | 2  | Copy 2                         | [1, 0, 0, 2, _, _, _, _]        |
| 4    | 3  | 3  | Copy 3                         | [1, 0, 0, 2, 3, _, _, _]        |
| 5    | 4  | 4  | Zero → duplicate if space      | [1, 0, 0, 2, 3, 0, 0, _]        |
| 6    | 5  | 6  | Copy 4                         | [1, 0, 0, 2, 3, 0, 0, 4]        |
| 7    | 6  | 7  | Copy 5                         | [1, 0, 0, 2, 3, 0, 0, 4] (unchanged, end reached) |
| 8    | 7  | —  | Last zero ignored (out of bounds) | [1, 0, 0, 2, 3, 0, 0, 4]     |

---

**Final Array:**  
[1, 0, 0, 2, 3, 0, 0, 4]  

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)` (in-place)


```
---

## 💡 Intuition Behind the Approach

Think about what happens when you see a zero:  

✅ You need to insert one **extra zero** right after it.  
✅ But inserting would **push elements rightward**, possibly overwriting others.  

👉 To avoid overwriting, we use a **two-pointer strategy from the back**:  

1. **Count the zeros** that will be duplicated.  
2. Use two pointers:  
   - `i` → original index  
   - `j` → "virtual new index" (accounting for duplicates)  
3. Traverse **backwards**:  
   - If `arr[i]` is non-zero → copy it to `arr[j]`  
   - If `arr[i]` is zero → write two zeros (`arr[j]` and `arr[j-1]`)  
4. Stop when `j` runs past the array.  

🔑 **Key Idea:** Process from **end to start** so that future elements don’t get overwritten.  

---

## Algorithm: Duplicate Zeros

**Goal:** Modify the given array in-place so that each `0` is duplicated, and the rest of the elements are shifted to the right.  
> Elements that go beyond the length of the array are **discarded**.

---

### Step-by-Step Explanation

1. **Understand the shifting problem**  
   - When we duplicate a zero, it pushes all subsequent elements one position to the right.  
   - If we do this naively from left to right, we’ll overwrite elements we haven’t processed yet.

2. **Count the zeros to be duplicated**  
   - First, traverse the array to count how many zeros **will actually be duplicated** without exceeding the array length.

3. **Use two pointers**  
   - One pointer (`i`) will move over the **original array** from the end.  
   - Another pointer (`j`) will represent the **new position** of elements after duplication (starting from the end).

4. **Start from the end to avoid overwriting**  
   - Begin from the last original index and move backwards.  
   - If `arr[i]` is not zero → copy it to `arr[j]`.  
   - If `arr[i]` is zero → write zero twice (duplicate) in `arr[j]` and `arr[j-1]`.

5. **Stop when we fill the array**  
   - Since `j` can exceed the array’s bounds, only fill elements when `j < arr.length`.

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
using namespace std;

class Solution {
public:
    void duplicateZeros(vector<int>& arr) {
        int n = arr.size();
        int zeros = 0;
        for (int num : arr) {
            if (num == 0) zeros++;
        }
        int i = n - 1, j = n + zeros - 1;
        while (i >= 0) {
            if (arr[i] != 0) {
                if (j < n) arr[j] = arr[i];
            } else {
                if (j < n) arr[j] = 0;
                j--;
                if (j < n) arr[j] = 0;
            }
            i--;
            j--;
        }
    }
};

int main() {
    int n;
    cout << "Enter number of elements: ";
    cin >> n;
    vector<int> arr(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> arr[i];
    Solution sol;
    sol.duplicateZeros(arr);
    cout << "After duplicating zeros: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
    return 0;
}


```
---

### **Java**
```java

import java.util.Scanner;

class Solution {
    public void duplicateZeros(int[] arr) {
        int n = arr.length;
        int zeros = 0;
        for (int num : arr) {
            if (num == 0) zeros++;
        }
        int i = n - 1, j = n + zeros - 1;
        while (i >= 0) {
            if (arr[i] != 0) {
                if (j < n) arr[j] = arr[i];
            } else {
                if (j < n) arr[j] = 0;
                j--;
                if (j < n) arr[j] = 0;
            }
            i--;
            j--;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) arr[i] = sc.nextInt();
        Solution sol = new Solution();
        sol.duplicateZeros(arr);
        System.out.print("After duplicating zeros: ");
        for (int num : arr) System.out.print(num + " ");
        System.out.println();
    }
}

```

---

### **Python**
```python

class Solution:
    def duplicateZeros(self, arr):
        n = len(arr)
        zeros = arr.count(0)
        i, j = n - 1, n + zeros - 1
        while i >= 0:
            if arr[i] != 0:
                if j < n:
                    arr[j] = arr[i]
            else:
                if j < n:
                    arr[j] = 0
                j -= 1
                if j < n:
                    arr[j] = 0
            i -= 1
            j -= 1

if __name__ == "__main__":
    n = int(input("Enter number of elements: "))
    arr = list(map(int, input("Enter elements: ").split()))
    sol = Solution()
    sol.duplicateZeros(arr)
    print("After duplicating zeros:", *arr)

```

---

### **JavaScript**
```javascript

const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    duplicateZeros(arr) {
        let n = arr.length;
        let zeros = arr.filter(x => x === 0).length;
        let i = n - 1, j = n + zeros - 1;
        while (i >= 0) {
            if (arr[i] !== 0) {
                if (j < n) arr[j] = arr[i];
            } else {
                if (j < n) arr[j] = 0;
                j--;
                if (j < n) arr[j] = 0;
            }
            i--;
            j--;
        }
    }
}

readline.question("Enter number of elements: ", (nStr) => {
    readline.question("Enter elements (space-separated): ", (arrStr) => {
        let arr = arrStr.trim().split(" ").map(Number);
        const sol = new Solution();
        sol.duplicateZeros(arr);
        console.log("After duplicating zeros:", arr.join(" "));
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




