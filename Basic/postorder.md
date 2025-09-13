# Binary Tree Postorder Traversal

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given the `root` of a binary tree, return the **postorder traversal** of its nodes' values.

**Postorder Traversal Order:**

1. Traverse the **left subtree**.
2. Traverse the **right subtree**.
3. Visit the **root** node.

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
\[3,2,1]

**Explanation:**
Postorder → Left → Right → Root
3 → 2 → 1

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

👉 Postorder traversal means:

1. Visit everything in the **left** subtree.
2. Visit everything in the **right** subtree.
3. Finally, visit the **root**.

There are **two common approaches**:

- **Recursive:** Straightforward using definition.
- **Iterative:** Use two stacks or modified preorder trick.

✅ Both work in `O(n)` time where `n` is the number of nodes.

---

## 📚 Algorithm Explanation

### Recursive Postorder:

1. If root is `null`, return.
2. Recursively traverse left subtree.
3. Recursively traverse right subtree.
4. Add `root.val` to result.

### Iterative Postorder (Two Stacks):

1. Push root into stack1.
2. Pop node from stack1, push into stack2.

   - Push its left and right children into stack1.

3. At the end, stack2 has postorder sequence.

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
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int> result;
        postorder(root, result);
        return result;
    }
private:
    void postorder(TreeNode* node, vector<int>& res) {
        if (!node) return;
        postorder(node->left, res);
        postorder(node->right, res);
        res.push_back(node->val);
    }
};

// Driver code
int main() {
    TreeNode* root = new TreeNode(1);
    root->right = new TreeNode(2);
    root->right->left = new TreeNode(3);

    Solution sol;
    vector<int> ans = sol.postorderTraversal(root);
    cout << "Postorder Traversal: ";
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
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        postorder(root, res);
        return res;
    }
    private void postorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        postorder(node.left, res);
        postorder(node.right, res);
        res.add(node.val);
    }
}

public class Main {
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        Solution sol = new Solution();
        System.out.println("Postorder Traversal: " + sol.postorderTraversal(root));
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
    def postorderTraversal(self, root):
        res = []
        def postorder(node):
            if not node: return
            postorder(node.left)
            postorder(node.right)
            res.append(node.val)
        postorder(root)
        return res

# Driver
if __name__ == "__main__":
    root = TreeNode(1)
    root.right = TreeNode(2)
    root.right.left = TreeNode(3)
    sol = Solution()
    print("Postorder Traversal:", sol.postorderTraversal(root))
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
  postorderTraversal(root) {
    const res = [];
    function postorder(node) {
      if (!node) return;
      postorder(node.left);
      postorder(node.right);
      res.push(node.val);
    }
    postorder(root);
    return res;
  }
}

// Driver
let root = new TreeNode(1);
root.right = new TreeNode(2);
root.right.left = new TreeNode(3);

const sol = new Solution();
console.log("Postorder Traversal:", sol.postorderTraversal(root));
```

---

## 🧪 Tests You Can Try

Input: root = \[1,null,2,3]
Output: \[3,2,1]

Input: root = \[]
Output: \[]

Input: root = \[1]
Output: \[1]

Input: root = \[1,2,3,4,5]
Output: \[4,5,2,3,1]

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
