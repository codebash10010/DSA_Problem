# Binary Tree Zigzag Level Order Traversal

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given the `root` of a binary tree, return the **zigzag level order traversal** of its nodes' values.
(i.e., from left to right, then right to left for the next level and alternate between).

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
\[\[3],\[20,9],\[15,7]]

**Explanation:**

- Level 1 → \[3]
- Level 2 → reversed → \[20,9]
- Level 3 → normal → \[15,7]

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

👉 This is just **Level Order Traversal with alternating directions**.

1. Perform a **BFS traversal** using a queue.
2. For each level, check if we need to reverse:

   - Odd level → left to right
   - Even level → right to left

3. Alternate the direction after every level.

✅ Runs in `O(n)` time where `n` is number of nodes.

---

## 📚 Algorithm Explanation

1. Initialize queue with root.
2. Maintain a boolean `leftToRight = true`.
3. For each level:

   - Extract all nodes.
   - Append values to level list.
   - If `!leftToRight`, reverse the level list.
   - Flip `leftToRight` for next iteration.

4. Append all levels to result.

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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> result;
        if (!root) return result;
        queue<TreeNode*> q;
        q.push(root);
        bool leftToRight = true;
        while (!q.empty()) {
            int size = q.size();
            vector<int> level(size);
            for (int i = 0; i < size; i++) {
                TreeNode* node = q.front(); q.pop();
                int idx = leftToRight ? i : (size - 1 - i);
                level[idx] = node->val;
                if (node->left) q.push(node->left);
                if (node->right) q.push(node->right);
            }
            result.push_back(level);
            leftToRight = !leftToRight;
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
    auto ans = sol.zigzagLevelOrder(root);
    cout << "Zigzag Level Order Traversal: ";
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
    public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;

        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        boolean leftToRight = true;

        while (!q.isEmpty()) {
            int size = q.size();
            Integer[] level = new Integer[size];
            for (int i = 0; i < size; i++) {
                TreeNode node = q.poll();
                int idx = leftToRight ? i : (size - 1 - i);
                level[idx] = node.val;
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
            res.add(Arrays.asList(level));
            leftToRight = !leftToRight;
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
        System.out.println("Zigzag Level Order Traversal: " + sol.zigzagLevelOrder(root));
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
    def zigzagLevelOrder(self, root):
        if not root: return []
        res, q, leftToRight = [], deque([root]), True
        while q:
            size = len(q)
            level = [0] * size
            for i in range(size):
                node = q.popleft()
                idx = i if leftToRight else size - 1 - i
                level[idx] = node.val
                if node.left: q.append(node.left)
                if node.right: q.append(node.right)
            res.append(level)
            leftToRight = not leftToRight
        return res

# Driver
if __name__ == "__main__":
    root = TreeNode(3)
    root.left = TreeNode(9)
    root.right = TreeNode(20)
    root.right.left = TreeNode(15)
    root.right.right = TreeNode(7)

    sol = Solution()
    print("Zigzag Level Order Traversal:", sol.zigzagLevelOrder(root))
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
  zigzagLevelOrder(root) {
    if (!root) return [];
    const res = [];
    const q = [root];
    let leftToRight = true;

    while (q.length > 0) {
      const size = q.length;
      const level = new Array(size);
      for (let i = 0; i < size; i++) {
        const node = q.shift();
        const idx = leftToRight ? i : size - 1 - i;
        level[idx] = node.val;
        if (node.left) q.push(node.left);
        if (node.right) q.push(node.right);
      }
      res.push(level);
      leftToRight = !leftToRight;
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
console.log("Zigzag Level Order Traversal:", sol.zigzagLevelOrder(root));
```

---

## 🧪 Tests You Can Try

Input: root = \[3,9,20,null,null,15,7]
Output: \[\[3],\[20,9],\[15,7]]

Input: root = \[1]
Output: \[\[1]]

Input: root = \[]
Output: \[]

Input: root = \[1,2,3,4,5,6,7]
Output: \[\[1],\[3,2],\[4,5,6,7]]

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
