# Binary Tree Inorder Traversal

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given the `root` of a binary tree, return the **inorder traversal** of its nodes' values.

**Inorder Traversal Order:**

1. Traverse the **left subtree**.
2. Visit the **root** node.
3. Traverse the **right subtree**.

---

## 📌 Constraints

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

---

## 📌 Examples

### Example 1

**Input:**
root = \[1,null,2,3]

**Output:**
\[1,3,2]

**Explanation:**
Inorder → Left → Root → Right
1 → 3 → 2

---

### Example 2

**Input:**
root = \[]

**Output:**
\[]

---

### Example 3

**Input:**
root = \[1]

**Output:**
\[1]

---

## 💡 Intuition Behind the Approach

👉 Inorder traversal means:

1. Traverse the **left** subtree first.
2. Visit the **root** node.
3. Traverse the **right** subtree.

There are **two common approaches**:

- **Recursive:** Simple and clean.
- **Iterative:** Use a stack to simulate recursion.

✅ Both work in `O(n)` time where `n` is the number of nodes.

---

## 📚 Algorithm Explanation

### Recursive Inorder:

1. If root is `null`, return.
2. Recursively traverse left subtree.
3. Add `root.val` to result.
4. Recursively traverse right subtree.

### Iterative Inorder:

1. Use a stack.
2. Push all left children until null.
3. Pop node, add to result, then move to its right child.

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
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> result;
        inorder(root, result);
        return result;
    }
private:
    void inorder(TreeNode* node, vector<int>& res) {
        if (!node) return;
        inorder(node->left, res);
        res.push_back(node->val);
        inorder(node->right, res);
    }
};

// Driver code
int main() {
    TreeNode* root = new TreeNode(1);
    root->right = new TreeNode(2);
    root->right->left = new TreeNode(3);

    Solution sol;
    vector<int> ans = sol.inorderTraversal(root);
    cout << "Inorder Traversal: ";
    for (int x : ans) cout << x << " ";
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
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }
    private void inorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        inorder(node.left, res);
        res.add(node.val);
        inorder(node.right, res);
    }
}

public class Main {
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        Solution sol = new Solution();
        System.out.println("Inorder Traversal: " + sol.inorderTraversal(root));
    }
}
```

---

### Python

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def inorderTraversal(self, root):
        res = []
        def inorder(node):
            if not node: return
            inorder(node.left)
            res.append(node.val)
            inorder(node.right)
        inorder(root)
        return res

# Driver
if __name__ == "__main__":
    root = TreeNode(1)
    root.right = TreeNode(2)
    root.right.left = TreeNode(3)
    sol = Solution()
    print("Inorder Traversal:", sol.inorderTraversal(root))
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
  inorderTraversal(root) {
    const res = [];
    function inorder(node) {
      if (!node) return;
      inorder(node.left);
      res.push(node.val);
      inorder(node.right);
    }
    inorder(root);
    return res;
  }
}

// Driver
let root = new TreeNode(1);
root.right = new TreeNode(2);
root.right.left = new TreeNode(3);

const sol = new Solution();
console.log("Inorder Traversal:", sol.inorderTraversal(root));
```

---

## 🧪 Tests You Can Try

Input: root = \[1,null,2,3]
Output: \[1,3,2]

Input: root = \[]
Output: \[]

Input: root = \[1]
Output: \[1]

Input: root = \[1,2,3,4,5]
Output: \[4,2,5,1,3]

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
