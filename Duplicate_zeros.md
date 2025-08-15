# Duplicate Zeros - Multiple Language Implementations

This repository contains solutions for the **"Duplicate Zeros"** problem implemented in **C++**, **Java**, **Python**, and **JavaScript**.

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

## 📌 Input / Output Example

**Example 1:**
Input: arr = [1,0,2,3,0,4,5,0]
Output: [1,0,0,2,3,0,0,4]

yaml
Copy
Edit
**Explanation:**  
Every zero is duplicated, and elements are shifted right. Elements beyond the length of the array are not included.

---

**Example 2:**
Input: arr = [1,2,3]
Output: [1,2,3]

cpp
Copy
Edit
**Explanation:**  
No zeros are present, so the array remains unchanged.

---

## 📌 Implementations

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
    cout << "Enter the elements: ";
    for (int i = 0; i < n; i++) cin >> arr[i];

    Solution sol;
    sol.duplicateZeros(arr);

    cout << "After duplicating zeros: ";
    for (int num : arr) cout << num << " ";
    cout << endl;
}
Java
java
Copy
Edit
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
Python
python
Copy
Edit
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
JavaScript
javascript
Copy
Edit
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
🚀 How to Run
C++
bash
Copy
Edit
g++ solution.cpp -o solution
./solution
Java
bash
Copy
Edit
javac Main.java
java Main
Python
bash
Copy
Edit
python solution.py
JavaScript
bash
Copy
Edit
node solution.js
📚 Algorithm Explanation
We use a two-pointer approach from the end:

Count the total number of zeros in the array.

Use two pointers:

i → points to the current element in the original array.

j → points to the position in the "virtual" extended array (original length + zeros count).

Traverse backward:

If arr[i] is not zero, copy it to arr[j] if j < n.

If arr[i] is zero, write zero twice (if j < n) and adjust j.

Stop when i reaches the beginning.

Time Complexity: O(n)
Space Complexity: O(1)