Here’s a detailed `.md` documentation for **LeetCode 542: 01 Matrix** in the style you like:

---

```markdown
# 01 Matrix - (LeetCode :- 542)

## 🏢 Companies Asked  
Amazon, Google, Facebook, Microsoft, etc.  
👉 [Watch on YouTube](https://www.youtube.com/watch?v=Ezj3VDOfd5I) :contentReference[oaicite:0]{index=0}  

---

## 🔗 Problem Link  
You can find the original problem here:  
👉 https://leetcode.com/problems/01-matrix/ :contentReference[oaicite:1]{index=1}  

---

## 📝 Problem Statement

You are given a binary matrix `mat` of size `m x n` (elements are 0 or 1).  
Return a matrix of the same size where for each cell `(i, j)`, the value is the **distance to the nearest 0** in `mat`.  
Distance is measured in terms of the number of steps (edges) in the grid: up, down, left, right (i.e. Manhattan moves).  

---

## 📌 Constraints

- `m == mat.length`  
- `n == mat[i].length`  
- `1 <= m, n <= 10⁴` (though usually both dimensions multiply to manageable sizes)  
- `mat[i][j]` is either `0` or `1`  
- At least one `0` exists in the matrix  

---

## 📌 Examples

### Example 1  
**Input:**  
```

mat = [
[0,0,0],
[0,1,0],
[0,0,0]
]

```
**Output:**  
```

[
[0,0,0],
[0,1,0],
[0,0,0]
]

```

---

### Example 2  
**Input:**  
```

mat = [
[0,0,0],
[0,1,0],
[1,1,1]
]

```
**Output:**  
```

[
[0,0,0],
[0,1,0],
[1,2,1]
]

````

---

## 💡 Intuition & Approaches

### Approach 1: Multi-source BFS (Recommended)

- Think of all `0` cells as **sources** and run a BFS outward from them simultaneously.
- Initialize a queue with all positions `(i, j)` where `mat[i][j] == 0`.
- Maintain a `dist` matrix, initialize `dist[i][j] = 0` for those zero cells, and `∞` (or large) for `1` cells.
- BFS layer by layer: for each popped cell, try its 4 neighbors — if a neighbor’s current `dist` > `current_dist + 1`, update it and push neighbor.
- This ensures the nearest zero distance is found, and runs in `O(m * n)` time.  
- This is a **multi-source BFS** problem. :contentReference[oaicite:2]{index=2}

### Approach 2: Dynamic Programming (Two Passes)

- First pass (top-left → bottom-right):  
  For each cell, take minimum of top neighbor + 1, left neighbor + 1.  
- Second pass (bottom-right → top-left):  
  For each cell, compare with bottom neighbor + 1, right neighbor + 1.  
- Combined passes propagate distances in all directions.  
- This works but must start with large default distances for `1` cells. :contentReference[oaicite:3]{index=3}

---

## ⏱ Complexity Analysis

- **Time Complexity:** `O(m * n)`  
- **Space Complexity:** `O(m * n)` (for distance matrix + queue)  

---

## 💻 Implementations (with Driver Code for User Input)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<vector<int>> updateMatrix(vector<vector<int>>& mat) {
        int m = mat.size();
        int n = mat[0].size();
        vector<vector<int>> dist(m, vector<int>(n, INT_MAX));
        queue<pair<int,int>> q;

        // Initialize queue with all zero cells
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    dist[i][j] = 0;
                    q.push({i, j});
                }
            }
        }

        vector<int> dirs = {0,1, 1,0, 0,-1, -1,0};
        while (!q.empty()) {
            auto [r, c] = q.front(); q.pop();
            for (int k = 0; k < 4; k++) {
                int nr = r + dirs[2*k];
                int nc = c + dirs[2*k+1];
                if (nr < 0 || nr >= m || nc < 0 || nc >= n) continue;
                if (dist[nr][nc] > dist[r][c] + 1) {
                    dist[nr][nc] = dist[r][c] + 1;
                    q.push({nr, nc});
                }
            }
        }
        return dist;
    }
};

int main() {
    int m, n;
    cout << "Enter rows and cols: ";
    cin >> m >> n;
    vector<vector<int>> mat(m, vector<int>(n));
    cout << "Enter matrix row by row (0/1):\n";
    for (int i = 0; i < m; i++)
        for (int j = 0; j < n; j++)
            cin >> mat[i][j];

    Solution sol;
    auto ans = sol.updateMatrix(mat);
    cout << "Distance matrix:\n";
    for (auto &row : ans) {
        for (int x : row) cout << x << " ";
        cout << "\n";
    }
    return 0;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public int[][] updateMatrix(int[][] mat) {
        int m = mat.length, n = mat[0].length;
        int[][] dist = new int[m][n];
        for (int[] row : dist) Arrays.fill(row, Integer.MAX_VALUE);
        Queue<int[]> q = new LinkedList<>();

        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (mat[i][j] == 0) {
                    dist[i][j] = 0;
                    q.offer(new int[]{i, j});
                }
            }
        }

        int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
        while (!q.isEmpty()) {
            int[] cell = q.poll();
            int r = cell[0], c = cell[1];
            for (int[] d : dirs) {
                int nr = r + d[0], nc = c + d[1];
                if (nr < 0 || nr >= m || nc < 0 || nc >= n) continue;
                if (dist[nr][nc] > dist[r][c] + 1) {
                    dist[nr][nc] = dist[r][c] + 1;
                    q.offer(new int[]{nr, nc});
                }
            }
        }
        return dist;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter rows and cols: ");
        int m = sc.nextInt(), n = sc.nextInt();
        int[][] mat = new int[m][n];
        System.out.println("Enter matrix (0 or 1):");
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                mat[i][j] = sc.nextInt();

        Solution sol = new Solution();
        int[][] res = sol.updateMatrix(mat);
        System.out.println("Distance matrix:");
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) 
                System.out.print(res[i][j] + " ");
            System.out.println();
        }
    }
}
```

---

### **Python**

```python
from collections import deque

class Solution:
    def updateMatrix(self, mat):
        m, n = len(mat), len(mat[0])
        dist = [[float('inf')] * n for _ in range(m)]
        q = deque()

        # Initialize
        for i in range(m):
            for j in range(n):
                if mat[i][j] == 0:
                    dist[i][j] = 0
                    q.append((i, j))

        dirs = [(1,0),(-1,0),(0,1),(0,-1)]
        while q:
            r, c = q.popleft()
            for dr, dc in dirs:
                nr, nc = r + dr, c + dc
                if 0 <= nr < m and 0 <= nc < n:
                    if dist[nr][nc] > dist[r][c] + 1:
                        dist[nr][nc] = dist[r][c] + 1
                        q.append((nr, nc))

        return dist

if __name__ == "__main__":
    m, n = map(int, input("Enter rows and cols: ").split())
    mat = []
    print("Enter matrix rows:")
    for _ in range(m):
        row = list(map(int, input().split()))
        mat.append(row)
    sol = Solution()
    ans = sol.updateMatrix(mat)
    print("Distance matrix:")
    for row in ans:
        print(" ".join(str(x) for x in row))
```

---

### **JavaScript (Node.js)**

```javascript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout
});

class Solution {
    updateMatrix(mat) {
        const m = mat.length, n = mat[0].length;
        const dist = Array.from({length: m}, () => Array(n).fill(Infinity));
        const q = [];

        for (let i = 0; i < m; i++) {
            for (let j = 0; j < n; j++) {
                if (mat[i][j] === 0) {
                    dist[i][j] = 0;
                    q.push([i, j]);
                }
            }
        }

        const dirs = [[1,0],[-1,0],[0,1],[0,-1]];
        let idx = 0;
        while (idx < q.length) {
            const [r, c] = q[idx++];
            for (const [dr, dc] of dirs) {
                const nr = r + dr, nc = c + dc;
                if (nr < 0 || nr >= m || nc < 0 || nc >= n) continue;
                if (dist[nr][nc] > dist[r][c] + 1) {
                    dist[nr][nc] = dist[r][c] + 1;
                    q.push([nr, nc]);
                }
            }
        }

        return dist;
    }
}

readline.question("Enter rows and cols: ", (rc) => {
    const [m, n] = rc.trim().split(" ").map(Number);
    console.log(`Enter ${m} rows (each with ${n} elements):`);
    const mat = [];
    let count = 0;
    readline.on("line", (line) => {
        mat.push(line.trim().split(" ").map(Number));
        count++;
        if (count === m) {
            const sol = new Solution();
            const ans = sol.updateMatrix(mat);
            console.log("Distance matrix:");
            for (let row of ans) console.log(row.join(" "));
            readline.close();
        }
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





