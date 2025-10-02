# 863. All Nodes Distance K in Binary Tree

**Difficulty:** 🟠 Medium  
[🔗 Problem Link](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)

---

## 📝 Problem Statement

You are given:

- The root of a **binary tree**
- A **target node**
- An integer `k`

Return an array of all node values that are **exactly `k` edges away** from the target node.

The answer can be returned in any order.

---

## 📌 Constraints

- `1 <= n <= 500` (number of nodes in the tree)
- `0 <= Node.val <= 500`
- `All Node.val are unique`
- `0 <= k <= n`

---

## ✅ Examples

### Example 1

**Input:**  
```

root = [3,5,1,6,2,0,8,null,null,7,4]
target = 5
k = 2

```

**Output:**  
```

[7,4,1]

```

**Explanation:**  
From node `5`, the nodes at distance `2` are:
- `7` (via `2`)
- `4` (via `2`)
- `1` (via `3`)

---

### Example 2

**Input:**  
```

root = [1]
target = 1
k = 3

```

**Output:**  
```

[]

````

---

## 💡 Intuition

This is essentially a **graph traversal problem**:

- Each node has **up to 3 neighbors**:
  1. Left child
  2. Right child
  3. Parent (important!)

Steps:

1. Convert the tree into a **graph representation** by linking each node with its parent.
2. Run a **BFS from the target node**:
   - Level 0 → target node
   - Level 1 → its neighbors
   - Level k → desired nodes
3. Collect all nodes reached at distance `k`.

---

## 📚 Algorithm

1. **DFS traversal** of the tree to build a `parent` map.
2. Initialize BFS from `target`.
3. Keep track of visited nodes to prevent cycles.
4. Run BFS for `k` steps.
5. Return all nodes at level `k`.

---

## 💻 Implementations (with Driver Code)

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
public:
    vector<int> distanceK(TreeNode* root, TreeNode* target, int k) {
        unordered_map<TreeNode*, TreeNode*> parent;
        markParents(root, parent);

        unordered_set<TreeNode*> visited;
        queue<TreeNode*> q;
        q.push(target);
        visited.insert(target);

        int dist = 0;
        while (!q.empty()) {
            int size = q.size();
            if (dist == k) break;
            dist++;
            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front(); q.pop();
                for (TreeNode* nbr : {node->left, node->right, parent[node]}) {
                    if (nbr && !visited.count(nbr)) {
                        visited.insert(nbr);
                        q.push(nbr);
                    }
                }
            }
        }

        vector<int> result;
        while (!q.empty()) {
            result.push_back(q.front()->val);
            q.pop();
        }
        return result;
    }

private:
    void markParents(TreeNode* root, unordered_map<TreeNode*, TreeNode*>& parent) {
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            TreeNode* node = q.front(); q.pop();
            if (node->left) {
                parent[node->left] = node;
                q.push(node->left);
            }
            if (node->right) {
                parent[node->right] = node;
                q.push(node->right);
            }
        }
    }
};

// Driver (builds simple tree manually for test)
int main() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(5);
    root->right = new TreeNode(1);
    root->left->left = new TreeNode(6);
    root->left->right = new TreeNode(2);
    root->right->left = new TreeNode(0);
    root->right->right = new TreeNode(8);
    root->left->right->left = new TreeNode(7);
    root->left->right->right = new TreeNode(4);

    Solution sol;
    vector<int> ans = sol.distanceK(root, root->left, 2); // target = 5, k = 2
    for (int x : ans) cout << x << " ";
    cout << endl;
}
````

---

### **Java**

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        Map<TreeNode, TreeNode> parent = new HashMap<>();
        markParents(root, parent);

        Queue<TreeNode> q = new LinkedList<>();
        Set<TreeNode> visited = new HashSet<>();
        q.add(target);
        visited.add(target);

        int dist = 0;
        while (!q.isEmpty()) {
            int size = q.size();
            if (dist == k) break;
            dist++;
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                for (TreeNode nbr : Arrays.asList(node.left, node.right, parent.get(node))) {
                    if (nbr != null && !visited.contains(nbr)) {
                        visited.add(nbr);
                        q.add(nbr);
                    }
                }
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!q.isEmpty()) {
            result.add(q.poll().val);
        }
        return result;
    }

    private void markParents(TreeNode root, Map<TreeNode, TreeNode> parent) {
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        while (!q.isEmpty()) {
            TreeNode node = q.poll();
            if (node.left != null) {
                parent.put(node.left, node);
                q.add(node.left);
            }
            if (node.right != null) {
                parent.put(node.right, node);
                q.add(node.right);
            }
        }
    }
}

// Driver
public class Main {
    public static void main(String[] args) {
        TreeNode root = new TreeNode(3);
        root.left = new TreeNode(5);
        root.right = new TreeNode(1);
        root.left.left = new TreeNode(6);
        root.left.right = new TreeNode(2);
        root.right.left = new TreeNode(0);
        root.right.right = new TreeNode(8);
        root.left.right.left = new TreeNode(7);
        root.left.right.right = new TreeNode(4);

        Solution sol = new Solution();
        System.out.println(sol.distanceK(root, root.left, 2)); // target=5, k=2
    }
}
```

---

### **Python**

```python
from collections import deque, defaultdict

class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = self.right = None

class Solution:
    def distanceK(self, root, target, k):
        parent = {}

        def dfs(node, par=None):
            if node:
                parent[node] = par
                dfs(node.left, node)
                dfs(node.right, node)
        dfs(root)

        visited = set([target])
        q = deque([target])
        dist = 0

        while q:
            if dist == k:
                return [node.val for node in q]
            for _ in range(len(q)):
                node = q.popleft()
                for nbr in (node.left, node.right, parent[node]):
                    if nbr and nbr not in visited:
                        visited.add(nbr)
                        q.append(nbr)
            dist += 1

        return []

# Driver
if __name__ == "__main__":
    root = TreeNode(3)
    root.left = TreeNode(5)
    root.right = TreeNode(1)
    root.left.left = TreeNode(6)
    root.left.right = TreeNode(2)
    root.right.left = TreeNode(0)
    root.right.right = TreeNode(8)
    root.left.right.left = TreeNode(7)
    root.left.right.right = TreeNode(4)

    sol = Solution()
    ans = sol.distanceK(root, root.left, 2)  # target=5, k=2
    print(ans)
```

---

```javascript
const readline = require("readline");

class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = this.right = null;
    }
}

class Solution {
    distanceK(root, target, k) {
        const parent = new Map();

        // Step 1: DFS to build parent references
        function dfs(node, par = null) {
            if (!node) return;
            parent.set(node, par);
            dfs(node.left, node);
            dfs(node.right, node);
        }
        dfs(root);

        // Step 2: BFS
        let visited = new Set([target]);
        let queue = [target];
        let dist = 0;

        while (queue.length > 0) {
            if (dist === k) return queue.map(n => n.val);

            let size = queue.length;
            let next = [];
            for (let i = 0; i < size; i++) {
                let node = queue[i];
                for (let nbr of [node.left, node.right, parent.get(node)]) {
                    if (nbr && !visited.has(nbr)) {
                        visited.add(nbr);
                        next.push(nbr);
                    }
                }
            }
            queue = next;
            dist++;
        }
        return [];
    }
}

// ---------- Helper: Build Tree from level order input ----------
function buildTree(arr) {
    if (!arr.length || arr[0] === "null") return null;

    let root = new TreeNode(parseInt(arr[0]));
    let queue = [root];
    let i = 1;

    while (i < arr.length) {
        let node = queue.shift();
        if (arr[i] && arr[i] !== "null") {
            node.left = new TreeNode(parseInt(arr[i]));
            queue.push(node.left);
        }
        i++;
        if (i < arr.length && arr[i] && arr[i] !== "null") {
            node.right = new TreeNode(parseInt(arr[i]));
            queue.push(node.right);
        }
        i++;
    }
    return root;
}

// ---------- User Input via readline ----------
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout,
});

let inputLines = [];
console.log("Enter input in format:");
console.log("Tree (level order with null): 3 5 1 6 2 0 8 null null 7 4");
console.log("Target: 5");
console.log("K: 2");

rl.on("line", (line) => {
    inputLines.push(line.trim());
    if (inputLines.length === 3) {
        rl.close();
    }
});

rl.on("close", () => {
    const treeArr = inputLines[0].split(" ");
    const targetVal = parseInt(inputLines[1]);
    const k = parseInt(inputLines[2]);

    const root = buildTree(treeArr);

    // Find target node by BFS
    let target = null;
    let q = [root];
    while (q.length) {
        let node = q.shift();
        if (!node) continue;
        if (node.val === targetVal) {
            target = node;
            break;
        }
        q.push(node.left);
        q.push(node.right);
    }

    if (!target) {
        console.log("Target not found in tree");
        return;
    }

    const sol = new Solution();
    console.log("Nodes at distance", k, ":", sol.distanceK(root, target, k));
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





## ⏱️ Complexity Analysis

* **Time Complexity:** `O(n)` (we traverse the tree + BFS).
* **Space Complexity:** `O(n)` (for parent map, visited set, BFS queue).

---

## 🙏 Thanks
Thanks for checking out this repository ❤️  
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀  

---