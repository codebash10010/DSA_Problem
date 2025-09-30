# 1361. Validate Binary Tree Nodes


## 🏢 Companies Asked :- DoorDash✯, TikTok✯, Facebook✯, Amazon✯, Adobe✯, Google, Goldman Sachs, Microsoft, Apple, DE Shaw, Bloomberg

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium  


[🔗 Problem Link](https://leetcode.com/problems/validate-binary-tree-nodes/)

---

## 📝 Problem Statement

You are given `n` binary tree nodes numbered from `0` to `n - 1`.

- Each node `i` has:
  - a left child: `leftChild[i]`
  - a right child: `rightChild[i]`

If a node has no child, its entry is `-1`.

Return `true` **iff** all the given nodes form **exactly one valid binary tree**.

---

## 📌 Constraints

- `1 <= n <= 10⁴`
- `leftChild.length == rightChild.length == n`
- `-1 <= leftChild[i], rightChild[i] <= n - 1`

---

## ✅ Examples

### Example 1

**Input:**  
```

n = 4
leftChild  = [1, -1, 3, -1]
rightChild = [2, -1, -1, -1]

```

**Output:**  
```

true

```

**Explanation:**  
The structure is:
```

```
0
```

/ 
1   2
/
3

```
This is a valid binary tree.

---

### Example 2

**Input:**  
```

n = 4
leftChild  = [1, -1, 3, -1]
rightChild = [2, 3, -1, -1]

```

**Output:**  
```

false

```

**Explanation:**  
Node `3` has **two parents**, so it's invalid.

---

### Example 3

**Input:**  
```

n = 2
leftChild  = [1, 0]
rightChild = [-1, -1]

```

**Output:**  
```

false

````

**Explanation:**  
This forms a cycle, not a tree.

---

## 💡 Intuition

For the nodes to form **one valid binary tree**, we need to satisfy three conditions:

1. **Only one root exists**  
   - Every node except one must have exactly one parent.  
   - The node with no parent is the **root**.  

2. **No node has multiple parents**  
   - If any node appears as a child more than once → invalid.  

3. **All nodes are connected (no cycles, no disconnected parts)**  
   - Starting from the root, we should be able to visit all `n` nodes exactly once.

This is essentially a **graph validation** problem.

---

## 📚 Algorithm

1. Count **indegree** of each node:
   - If any node has `indegree > 1`, return `false`.
2. Find the **root** (the one with `indegree == 0`):
   - If not exactly one root, return `false`.
3. Run **DFS/BFS** from root:
   - Keep a visited set.
   - If we revisit a node → cycle → `false`.
   - At the end, if not all `n` nodes are visited → disconnected → `false`.
4. Otherwise, return `true`.

---

## 💻 Implementations (with Driver Code)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    bool validateBinaryTreeNodes(int n, vector<int>& leftChild, vector<int>& rightChild) {
        vector<int> indegree(n, 0);

        for (int i = 0; i < n; i++) {
            if (leftChild[i] != -1) {
                if (++indegree[leftChild[i]] > 1) return false;
            }
            if (rightChild[i] != -1) {
                if (++indegree[rightChild[i]] > 1) return false;
            }
        }

        int root = -1;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                if (root == -1) root = i;
                else return false; // more than one root
            }
        }
        if (root == -1) return false; // no root

        // BFS traversal
        vector<bool> visited(n, false);
        queue<int> q;
        q.push(root);
        visited[root] = true;

        int count = 0;
        while (!q.empty()) {
            int node = q.front(); q.pop();
            count++;
            if (leftChild[node] != -1) {
                if (visited[leftChild[node]]) return false;
                visited[leftChild[node]] = true;
                q.push(leftChild[node]);
            }
            if (rightChild[node] != -1) {
                if (visited[rightChild[node]]) return false;
                visited[rightChild[node]] = true;
                q.push(rightChild[node]);
            }
        }

        return count == n;
    }
};

// Driver
int main() {
    int n;
    cout << "Enter n: ";
    cin >> n;
    vector<int> leftChild(n), rightChild(n);

    cout << "Enter leftChild array: ";
    for (int i = 0; i < n; i++) cin >> leftChild[i];
    cout << "Enter rightChild array: ";
    for (int i = 0; i < n; i++) cin >> rightChild[i];

    Solution sol;
    cout << (sol.validateBinaryTreeNodes(n, leftChild, rightChild) ? "true" : "false") << endl;
}
````

---

### **Java**

```java
import java.util.*;

class Solution {
    public boolean validateBinaryTreeNodes(int n, int[] leftChild, int[] rightChild) {
        int[] indegree = new int[n];

        for (int i = 0; i < n; i++) {
            if (leftChild[i] != -1 && ++indegree[leftChild[i]] > 1) return false;
            if (rightChild[i] != -1 && ++indegree[rightChild[i]] > 1) return false;
        }

        int root = -1;
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                if (root == -1) root = i;
                else return false;
            }
        }
        if (root == -1) return false;

        boolean[] visited = new boolean[n];
        Queue<Integer> q = new LinkedList<>();
        q.add(root);
        visited[root] = true;
        int count = 0;

        while (!q.isEmpty()) {
            int node = q.poll();
            count++;
            if (leftChild[node] != -1) {
                if (visited[leftChild[node]]) return false;
                visited[leftChild[node]] = true;
                q.add(leftChild[node]);
            }
            if (rightChild[node] != -1) {
                if (visited[rightChild[node]]) return false;
                visited[rightChild[node]] = true;
                q.add(rightChild[node]);
            }
        }

        return count == n;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter n: ");
        int n = sc.nextInt();
        int[] leftChild = new int[n];
        int[] rightChild = new int[n];

        System.out.println("Enter leftChild array: ");
        for (int i = 0; i < n; i++) leftChild[i] = sc.nextInt();
        System.out.println("Enter rightChild array: ");
        for (int i = 0; i < n; i++) rightChild[i] = sc.nextInt();

        Solution sol = new Solution();
        System.out.println(sol.validateBinaryTreeNodes(n, leftChild, rightChild));
    }
}
```

---

### **Python**

```python
from collections import deque

class Solution:
    def validateBinaryTreeNodes(self, n, leftChild, rightChild):
        indegree = [0] * n
        for i in range(n):
            if leftChild[i] != -1:
                indegree[leftChild[i]] += 1
                if indegree[leftChild[i]] > 1:
                    return False
            if rightChild[i] != -1:
                indegree[rightChild[i]] += 1
                if indegree[rightChild[i]] > 1:
                    return False

        root = -1
        for i in range(n):
            if indegree[i] == 0:
                if root == -1:
                    root = i
                else:
                    return False
        if root == -1:
            return False

        visited = [False] * n
        q = deque([root])
        visited[root] = True
        count = 0

        while q:
            node = q.popleft()
            count += 1
            for child in (leftChild[node], rightChild[node]):
                if child != -1:
                    if visited[child]:
                        return False
                    visited[child] = True
                    q.append(child)

        return count == n


if __name__ == "__main__":
    n = int(input("Enter n: "))
    leftChild = list(map(int, input("Enter leftChild array: ").split()))
    rightChild = list(map(int, input("Enter rightChild array: ").split()))

    sol = Solution()
    print(sol.validateBinaryTreeNodes(n, leftChild, rightChild))
```

---

### **JavaScript (Node.js)**

```javascript
class Solution {
    validateBinaryTreeNodes(n, leftChild, rightChild) {
        const indegree = new Array(n).fill(0);

        for (let i = 0; i < n; i++) {
            if (leftChild[i] !== -1 && ++indegree[leftChild[i]] > 1) return false;
            if (rightChild[i] !== -1 && ++indegree[rightChild[i]] > 1) return false;
        }

        let root = -1;
        for (let i = 0; i < n; i++) {
            if (indegree[i] === 0) {
                if (root === -1) root = i;
                else return false;
            }
        }
        if (root === -1) return false;

        const visited = new Array(n).fill(false);
        let q = [root];
        visited[root] = true;
        let count = 0;

        while (q.length > 0) {
            const node = q.shift();
            count++;
            for (let child of [leftChild[node], rightChild[node]]) {
                if (child !== -1) {
                    if (visited[child]) return false;
                    visited[child] = true;
                    q.push(child);
                }
            }
        }

        return count === n;
    }
}

// Driver
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

readline.question("Enter n: ", (nStr) => {
    const n = parseInt(nStr);
    readline.question("Enter leftChild array: ", (leftStr) => {
        const leftChild = leftStr.trim().split(" ").map(Number);
        readline.question("Enter rightChild array: ", (rightStr) => {
            const rightChild = rightStr.trim().split(" ").map(Number);
            const sol = new Solution();
            console.log(sol.validateBinaryTreeNodes(n, leftChild, rightChild));
            readline.close();
        });
    });
});
```

---

## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)` (we process each node and edge once).
* **Space Complexity:** `O(n)` (for indegree + visited + BFS queue).

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

## 🔗 Related Problems

* [261. Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/)
* [200. Number of Islands](https://leetcode.com/problems/number-of-islands/)
* [207. Course Schedule](https://leetcode.com/problems/course-schedule/)

---

## 🙏 Thanks
Thanks for checking out this repository ❤️  
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀  

---