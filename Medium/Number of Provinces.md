### 1️⃣ Number of Provinces - (LeetCode: 547)

**File:** `number_of_provinces.md`

````markdown
# Number of Provinces - (LeetCode :- 547)

## 🏢 Companies Asked :- Amazon ✯, Google ✯, Microsoft ✯, Facebook ✯, Adobe ✯

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium  

[🔗 Problem Link](https://leetcode.com/problems/number-of-provinces/)

---

## 🧩 Problem Statement
You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `i`th city and the `j`th city are directly connected, and `isConnected[i][j] = 0` otherwise.  
Return *the total number of provinces* (groups of directly or indirectly connected cities).

---

## 💡 Intuition
This is essentially a **graph connected components** problem.  
- Each city is a node.  
- A province is a connected component in the graph.  

DFS or BFS can traverse each component.

---

## ⚙️ Approach
1. Initialize a visited array for all cities.  
2. Iterate over all cities:
   - If a city is not visited, do DFS/BFS from it.
   - Count the number of DFS/BFS calls → number of provinces.  

---

## 🧩 Code Implementations

### 🧱 C++
```cpp
#include <bits/stdc++.h>
using namespace std;

void dfs(int u, vector<vector<int>>& isConnected, vector<bool>& visited){
    visited[u] = true;
    for(int v = 0; v < isConnected.size(); v++){
        if(isConnected[u][v] && !visited[v]){
            dfs(v, isConnected, visited);
        }
    }
}

int findCircleNum(vector<vector<int>>& isConnected) {
    int n = isConnected.size();
    vector<bool> visited(n, false);
    int provinces = 0;
    for(int i = 0; i < n; i++){
        if(!visited[i]){
            dfs(i, isConnected, visited);
            provinces++;
        }
    }
    return provinces;
}

int main() {
    int n;
    cin >> n;
    vector<vector<int>> isConnected(n, vector<int>(n));
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin >> isConnected[i][j];
    cout << findCircleNum(isConnected) << "\n";
    return 0;
}
````

### ☕ Java

```java
import java.util.*;

public class Main {
    static void dfs(int u, int[][] isConnected, boolean[] visited){
        visited[u] = true;
        for(int v=0; v<isConnected.length; v++){
            if(isConnected[u][v]==1 && !visited[v]){
                dfs(v, isConnected, visited);
            }
        }
    }

    public static int findCircleNum(int[][] isConnected){
        int n = isConnected.length;
        boolean[] visited = new boolean[n];
        int provinces = 0;
        for(int i=0;i<n;i++){
            if(!visited[i]){
                dfs(i,isConnected,visited);
                provinces++;
            }
        }
        return provinces;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] isConnected = new int[n][n];
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                isConnected[i][j] = sc.nextInt();
        System.out.println(findCircleNum(isConnected));
        sc.close();
    }
}
```

### 🐍 Python

```python
def dfs(u, isConnected, visited):
    visited[u] = True
    for v in range(len(isConnected)):
        if isConnected[u][v] == 1 and not visited[v]:
            dfs(v, isConnected, visited)

def findCircleNum(isConnected):
    n = len(isConnected)
    visited = [False]*n
    provinces = 0
    for i in range(n):
        if not visited[i]:
            dfs(i, isConnected, visited)
            provinces += 1
    return provinces

if __name__ == "__main__":
    n = int(input())
    isConnected = [list(map(int, input().split())) for _ in range(n)]
    print(findCircleNum(isConnected))
```

### ⚡ JavaScript

```javascript
function findCircleNum(isConnected) {
    const n = isConnected.length;
    const visited = Array(n).fill(false);

    function dfs(u){
        visited[u] = true;
        for(let v=0; v<n; v++){
            if(isConnected[u][v] && !visited[v]){
                dfs(v);
            }
        }
    }

    let provinces = 0;
    for(let i=0;i<n;i++){
        if(!visited[i]){
            dfs(i);
            provinces++;
        }
    }
    return provinces;
}

const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout
});

readline.question("Enter n: ", nStr => {
    const n = parseInt(nStr);
    const matrix = [];
    let rowCount = 0;

    console.log(`Enter ${n} rows of matrix space-separated:`);
    readline.on('line', line => {
        matrix.push(line.trim().split(' ').map(Number));
        rowCount++;
        if(rowCount === n){
            console.log(findCircleNum(matrix));
            readline.close();
        }
    });
});
```

---

## 🧪 Sample Run

**Input**

```
3
1 1 0
1 1 0
0 0 1
```

**Output**

```
2
```

---

## ⏱ Complexity

* **Time:** O(n²)
* **Space:** O(n)

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

