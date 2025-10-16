# Unique Paths - (LeetCode :- 62)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Facebook

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/unique-paths/description/)

---

## 🧩 Problem Statement

A robot is located at the **top-left corner** of an `m x n` grid. The robot can only move **down** or **right** at any point in time.

The robot is trying to reach the **bottom-right corner** of the grid.

Return **the number of possible unique paths** that the robot can take to reach the bottom-right corner.

---

## 💡 Intuition

* At any cell `(i,j)`, robot can come from **top `(i-1,j)`** or **left `(i,j-1)`**.
* Use **Dynamic Programming** to store number of paths to each cell.

---

## ⚙️ Approach

1. Create a 2D array `dp[m][n]`.
2. Initialize first row and first column as `1` (only one way to reach them).
3. For each cell `(i,j)`, `dp[i][j] = dp[i-1][j] + dp[i][j-1]`.
4. Return `dp[m-1][n-1]`.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int uniquePaths(int m, int n) {
    vector<vector<int>> dp(m, vector<int>(n,1));
    for(int i=1;i<m;i++){
        for(int j=1;j<n;j++){
            dp[i][j]=dp[i-1][j]+dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}

int main(){
    int m,n;
    cin >> m >> n;
    cout << uniquePaths(m,n) << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main{
    public static int uniquePaths(int m, int n){
        int[][] dp = new int[m][n];
        for(int i=0;i<m;i++) dp[i][0]=1;
        for(int j=0;j<n;j++) dp[0][j]=1;
        
        for(int i=1;i<m;i++){
            for(int j=1;j<n;j++){
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
            }
        }
        return dp[m-1][n-1];
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int m=sc.nextInt();
        int n=sc.nextInt();
        System.out.println(uniquePaths(m,n));
        sc.close();
    }
}
```

### 🐍 Python

```python
def uniquePaths(m,n):
    dp=[[1]*n for _ in range(m)]
    for i in range(1,m):
        for j in range(1,n):
            dp[i][j]=dp[i-1][j]+dp[i][j-1]
    return dp[m-1][n-1]

if __name__=="__main__":
    m,n=map(int,input().split())
    print(uniquePaths(m,n))
```

### ⚡ JavaScript

```javascript
const readline=require('readline').createInterface({
    input:process.stdin,
    output:process.stdout
});

function uniquePaths(m,n){
    const dp=Array.from({length:m},()=>Array(n).fill(1));
    for(let i=1;i<m;i++){
        for(let j=1;j<n;j++){
            dp[i][j]=dp[i-1][j]+dp[i][j-1];
        }
    }
    return dp[m-1][n-1];
}

let lines=[];
readline.on('line', line=>lines.push(line));
readline.on('close', ()=>{
    const [m,n]=lines[0].split(" ").map(Number);
    console.log(uniquePaths(m,n));
});
```

---

## ⏱ Complexity

* **Time:** O(m*n)
* **Space:** O(m*n)

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
