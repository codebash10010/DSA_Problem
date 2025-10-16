# Shortest Bridge - (LeetCode :- 934)

## 🏢 Companies Asked :- Google, Amazon, Microsoft, Facebook

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/shortest-bridge/)

---

## 🧩 Problem Statement

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

There are exactly **two islands** in `grid` (an island is a group of `1`s connected **4-directionally**).

You may **flip 0s to 1s** to connect the two islands to form one island.

Return the **smallest number of 0s you must flip** to connect the two islands.

---

## 📌 Constraints

* `n == grid.length == grid[i].length`
* `2 <= n <= 100`
* `grid[i][j]` is either `0` or `1`
* There are exactly **two islands** in `grid`.

---

## 📌 Example

### Example 1

Input:

```
grid = [[0,1],[1,0]]
```

Output: `1`

Explanation: Flip the 0 at (0,0) or (1,1) to connect the islands.

### Example 2

Input:

```
grid = [[0,1,0],[0,0,0],[0,0,1]]
```

Output: `2`

---

## 💡 Intuition

1. Find one of the islands using **DFS/BFS** and mark all its cells.
2. Start **BFS** from all cells of the first island to find the shortest path to the second island.
3. The BFS level when we first reach the second island gives the minimum flips required.

---

## ⚙️ Approach (Step-by-Step)

1. Loop through grid to find first `1` → start DFS to mark all cells of first island.
2. Use a queue to store all cells of first island.
3. Perform BFS from queue:

   * Expand to 4 neighbors.
   * If neighbor is second island → return distance.
   * Else, mark water as visited and continue BFS.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int n;
vector<vector<int>> grid;
vector<vector<int>> dirs = {{1,0},{-1,0},{0,1},{0,-1}};

void dfs(int i, int j, vector<vector<int>> &vis, queue<pair<int,int>> &q){
    if(i<0||j<0||i>=n||j>=n||vis[i][j]||grid[i][j]==0) return;
    vis[i][j]=1;
    q.push({i,j});
    for(auto d:dirs) dfs(i+d[0], j+d[1], vis, q);
}

int shortestBridge(vector<vector<int>> &grid){
    n = grid.size();
    vector<vector<int>> vis(n, vector<int>(n,0));
    queue<pair<int,int>> q;
    bool found=false;
    for(int i=0;i<n&&!found;i++){
        for(int j=0;j<n&&!found;j++){
            if(grid[i][j]==1){
                dfs(i,j,vis,q);
                found=true;
            }
        }
    }
    int steps=0;
    while(!q.empty()){
        int sz=q.size();
        while(sz--){
            auto [x,y]=q.front(); q.pop();
            for(auto d:dirs){
                int nx=x+d[0], ny=y+d[1];
                if(nx>=0&&ny>=0&&nx<n&&ny<n&&!vis[nx][ny]){
                    if(grid[nx][ny]==1) return steps;
                    vis[nx][ny]=1;
                    q.push({nx,ny});
                }
            }
        }
        steps++;
    }
    return -1;
}

int main(){
    cin >> n;
    grid.resize(n, vector<int>(n));
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            cin >> grid[i][j];
    cout << shortestBridge(grid) << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main {
    static int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
    
    static void dfs(int[][] grid, int[][] vis, Queue<int[]> q, int i, int j){
        int n = grid.length;
        if(i<0||j<0||i>=n||j>=n||vis[i][j]==1||grid[i][j]==0) return;
        vis[i][j]=1;
        q.add(new int[]{i,j});
        for(int[] d: dirs) dfs(grid, vis, q, i+d[0], j+d[1]);
    }
    
    public static int shortestBridge(int[][] grid){
        int n = grid.length;
        int[][] vis = new int[n][n];
        Queue<int[]> q = new LinkedList<>();
        boolean found=false;
        for(int i=0;i<n&&!found;i++){
            for(int j=0;j<n&&!found;j++){
                if(grid[i][j]==1){
                    dfs(grid, vis, q, i, j);
                    found=true;
                }
            }
        }
        int steps=0;
        while(!q.isEmpty()){
            int size = q.size();
            for(int s=0;s<size;s++){
                int[] cur = q.poll();
                int x=cur[0], y=cur[1];
                for(int[] d: dirs){
                    int nx=x+d[0], ny=y+d[1];
                    if(nx>=0 && ny>=0 && nx<n && ny<n && vis[nx][ny]==0){
                        if(grid[nx][ny]==1) return steps;
                        vis[nx][ny]=1;
                        q.add(new int[]{nx,ny});
                    }
                }
            }
            steps++;
        }
        return -1;
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] grid = new int[n][n];
        for(int i=0;i<n;i++)
            for(int j=0;j<n;j++)
                grid[i][j]=sc.nextInt();
        System.out.println(shortestBridge(grid));
        sc.close();
    }
}
```

### 🐍 Python

```python
from collections import deque

dirs = [(1,0),(-1,0),(0,1),(0,-1)]

def dfs(i,j,grid,vis,q):
    n=len(grid)
    if i<0 or j<0 or i>=n or j>=n or vis[i][j] or grid[i][j]==0:
        return
    vis[i][j]=1
    q.append((i,j))
    for dx,dy in dirs:
        dfs(i+dx,j+dy,grid,vis,q)

def shortestBridge(grid):
    n=len(grid)
    vis=[[0]*n for _ in range(n)]
    q=deque()
    found=False
    for i in range(n):
        if found: break
        for j in range(n):
            if grid[i][j]==1:
                dfs(i,j,grid,vis,q)
                found=True
                break
    steps=0
    while q:
        for _ in range(len(q)):
            x,y=q.popleft()
            for dx,dy in dirs:
                nx,ny=x+dx,y+dy
                if 0<=nx<n and 0<=ny<n and not vis[nx][ny]:
                    if grid[nx][ny]==1:
                        return steps
                    vis[nx][ny]=1
                    q.append((nx,ny))
        steps+=1
    return -1

if __name__=="__main__":
    n=int(input())
    grid=[list(map(int,input().split())) for _ in range(n)]
    print(shortestBridge(grid))
```

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

const dirs = [[1,0],[-1,0],[0,1],[0,-1]];

function dfs(i,j,grid,vis,q){
    const n=grid.length;
    if(i<0||j<0||i>=n||j>=n||vis[i][j]||grid[i][j]===0) return;
    vis[i][j]=1;
    q.push([i,j]);
    for(const [dx,dy] of dirs) dfs(i+dx,j+dy,grid,vis,q);
}

function shortestBridge(grid){
    const n=grid.length;
    const vis=Array.from({length:n},()=>Array(n).fill(0));
    const q=[];
    let found=false;
    for(let i=0;i<n && !found;i++){
        for(let j=0;j<n && !found;j++){
            if(grid[i][j]===1){
                dfs(i,j,grid,vis,q);
                found=true;
            }
        }
    }
    let steps=0;
    while(q.length){
        let size=q.length;
        for(let s=0;s<size;s++){
            const [x,y]=q.shift();
            for(const [dx,dy] of dirs){
                const nx=x+dx, ny=y+dy;
                if(nx>=0 && ny>=0 && nx<n && ny<n && vis[nx][ny]===0){
                    if(grid[nx][ny]===1) return steps;
                    vis[nx][ny]=1;
                    q.push([nx,ny]);
                }
            }
        }
        steps++;
    }
    return -1;
}

readline.question("Enter n: ", nLine => {
    const n = parseInt(nLine);
    const grid = [];
    let count=0;
    function readRow(){
        if(count<n){
            readline.question(`Enter row ${count+1}: `, row=>{
                grid.push(row.split(' ').map(Number));
                count++;
                readRow();
            });
        } else {
            console.log(shortestBridge(grid));
            readline.close();
        }
    }
    readRow();
});
```

---

## ⏱ Complexity

* **Time:** O(n²)
* **Space:** O(n²)

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