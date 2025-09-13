# Binary Tree Level Order Traversal

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given the `root` of a binary tree, return the **level order traversal** of its nodes' values.
(i.e., from left to right, level by level).

---

## 📌 Constraints

- The number of nodes in the tree is in the range `[0, 2000]`.
- `-1000 <= Node.val <= 1000`

---

## 📌 Examples

### Example 1

**Input:**
root = \[3,9,20,null,null,15,7]

**Output:**
\[\[3],\[9,20],\[15,7]]

**Explanation:**

- Level 1 → \[3]
- Level 2 → \[9,20]
- Level 3 → \[15,7]

---

### Example 2

**Input:**
root = \[1]

**Output:**
\[\[1]]

---

### Example 3

**Input:**
root = \[]

**Output:**
\[]

---

## 💡 Intuition Behind the Approach

👉 Level Order Traversal means **Breadth-First Search (BFS)**.

1. We explore the tree **level by level**.
2. Use a **queue** to keep track of nodes at each level.
3. For every node:

   - Pop from queue.
   - Add its children to queue.
   - Collect values level by level.

✅ Runs in `O(n)` time where `n` is number of nodes.

---

## 📚 Algorithm Explanation

1. If root is `null`, return empty list.
2. Initialize a queue with the root.
3. While queue is not empty:

   - Create a list for the current level.
   - For each node in queue:

     - Pop node.
     - Add its value to level list.
     - Push its left and right children if they exist.

   - Append level list to result.

---

## 💻 Implementations

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (!root) return result;
        queue<TreeNode*> q;
        q.push(root);
        while (!q.empty()) {
            int size = q.size();
            vector<int> level;
            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front(); q.pop();
                level.push_back(node->val);
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            result.push_back(level);
        }
        return result;
    }
};

// Driver code
int main() {
    TreeNode* root = new TreeNode(3);
    root->left = new TreeNode(9);
    root->right = new TreeNode(20);
    root->right->left = new TreeNode(15);
    root->right->right = new TreeNode(7);

    Solution sol;
    auto ans = sol.levelOrder(root);
    cout << "Level Order Traversal: ";
    for (auto &lvl : ans) {
        cout << "[";
        for (int x : lvl) cout << x << " ";
        cout << "]";
    }
}
```

---

### Java

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);

        while (!q.isEmpty()) {
            int size = q.size();
            List<Integer> level = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                level.add(node.val);
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
            res.add(level);
        }
        return res;
    }
}

public class Main {
    public static void main(String[] args) {
        TreeNode root = new TreeNode(3);
        root.left = new TreeNode(9);
        root.right = new TreeNode(20);
        root.right.left = new TreeNode(15);
        root.right.right = new TreeNode(7);

        Solution sol = new Solution();
        System.out.println("Level Order Traversal: " + sol.levelOrder(root));
    }
}
```

---

### Python

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def levelOrder(self, root):
        if not root: return []
        res, q = [], deque([root])
        while q:
            level = []
            for _ in range(len(q)):
                node = q.popleft()
                level.append(node.val)
                if node.left: q.append(node.left)
                if node.right: q.append(node.right)
            res.append(level)
        return res

# Driver
if __name__ == "__main__":
    root = TreeNode(3)
    root.left = TreeNode(9)
    root.right = TreeNode(20)
    root.right.left = TreeNode(15)
    root.right.right = TreeNode(7)

    sol = Solution()
    print("Level Order Traversal:", sol.levelOrder(root))
```

---

### JavaScript

```javascript
class TreeNode {
  constructor(val, left = null, right = null) {
    this.val = val;
    this.left = left;
    this.right = right;
  }
}

class Solution {
  levelOrder(root) {
    if (!root) return [];
    const res = [];
    const q = [root];
    while (q.length > 0) {
      const size = q.length;
      const level = [];
      for (let i = 0; i < size; i++) {
        const node = q.shift();
        level.push(node.val);
        if (node.left) q.push(node.left);
        if (node.right) q.push(node.right);
      }
      res.push(level);
    }
    return res;
  }
}

// Driver
let root = new TreeNode(3);
root.left = new TreeNode(9);
root.right = new TreeNode(20);
root.right.left = new TreeNode(15);
root.right.right = new TreeNode(7);

const sol = new Solution();
console.log("Level Order Traversal:", sol.levelOrder(root));
```

---

## 🧪 Tests You Can Try

Input: root = \[3,9,20,null,null,15,7]
Output: \[\[3],\[9,20],\[15,7]]

Input: root = \[1]
Output: \[\[1]]

Input: root = \[]
Output: \[]

Input: root = \[1,2,3,4,5,6,7]
Output: \[\[1],\[2,3],\[4,5,6,7]]

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

### **JavaScript (Node.js)**

```bash
node solution.js
```

---

## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀

---
