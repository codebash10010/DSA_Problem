# Can Make Arithmetic Progression From Sequence - (LeetCode :- 1502)

## 🏢 Companies Asked :- Amazon, Microsoft, Google, Adobe

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟢 Easy

[🔗 Problem Link](https://leetcode.com/problems/can-make-arithmetic-progression-from-sequence/)

---

## 🧩 Problem Statement

Given an array of numbers `arr`, return `true` if the **numbers can be rearranged** to form an **arithmetic progression**. Otherwise, return `false`.

An **arithmetic progression** is a sequence where the difference between consecutive elements is **constant**.

---

## 📌 Constraints

* `2 <= arr.length <= 1000`
* `-10^6 <= arr[i] <= 10^6`

---

## 📌 Example

### Example 1

Input:

```
arr = [3,5,1]
```

Output:

```
true
```

Explanation: Reordering `[1,3,5]` forms an arithmetic progression with difference 2.

### Example 2

Input:

```
arr = [1,2,4]
```

Output:

```
false
```

---

## 💡 Intuition

* Sort the array.
* Check if the difference between consecutive elements is the same.
* If yes → arithmetic progression exists.

---

## ⚙️ Approach (Step-by-Step)

1. Sort the array.
2. Compute `diff = arr[1] - arr[0]`.
3. Loop from index 1 to n-1:

   * If `arr[i] - arr[i-1] != diff` → return false.
4. Return true.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

bool canMakeArithmeticProgression(vector<int>& arr){
    sort(arr.begin(), arr.end());
    int diff = arr[1]-arr[0];
    for(int i=1;i<arr.size();i++){
        if(arr[i]-arr[i-1]!=diff) return false;
    }
    return true;
}

int main(){
    int n;
    cin >> n;
    vector<int> arr(n);
    for(int i=0;i<n;i++) cin >> arr[i];
    cout << (canMakeArithmeticProgression(arr) ? "true" : "false") << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main{
    public static boolean canMakeArithmeticProgression(int[] arr){
        Arrays.sort(arr);
        int diff = arr[1]-arr[0];
        for(int i=1;i<arr.length;i++){
            if(arr[i]-arr[i-1]!=diff) return false;
        }
        return true;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for(int i=0;i<n;i++) arr[i]=sc.nextInt();
        System.out.println(canMakeArithmeticProgression(arr));
        sc.close();
    }
}
```

### 🐍 Python

```python
def canMakeArithmeticProgression(arr):
    arr.sort()
    diff = arr[1]-arr[0]
    for i in range(1,len(arr)):
        if arr[i]-arr[i-1]!=diff:
            return False
    return True

if __name__=="__main__":
    n=int(input())
    arr=list(map(int,input().split()))
    print(canMakeArithmeticProgression(arr))
```

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

function canMakeArithmeticProgression(arr){
    arr.sort((a,b)=>a-b);
    let diff = arr[1]-arr[0];
    for(let i=1;i<arr.length;i++){
        if(arr[i]-arr[i-1]!==diff) return false;
    }
    return true;
}

readline.question("Enter array size and elements: ", line=>{
    let parts=line.trim().split(" ").map(Number);
    let n=parts[0];
    let arr=parts.slice(1);
    console.log(canMakeArithmeticProgression(arr));
    readline.close();
});
```

---

## ⏱ Complexity

* **Time:** O(n log n) → due to sorting
* **Space:** O(1) or O(n) depending on language sorting implementation

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