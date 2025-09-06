# Binary Tree Preorder Traversal

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 📝 Problem Statement

Given the `root` of a binary tree, return the **preorder traversal** of its nodes' values.

**Preorder Traversal Order:**

1. Visit **root** node.
2. Traverse the **left subtree**.
3. Traverse the **right subtree**.

---

## 📌 Constraints

- The number of nodes in the tree is in the range `[0, 100]`.
- `-100 <= Node.val <= 100`

---

## 📌 Examples

### Example 1

**Input:**  
root = [1,null,2,3]

**Output:**  
[1,2,3]

**Explanation:**  
Preorder → Visit root → Left → Right  
1 → 2 → 3

---

### Example 2

**Input:**  
root = []

**Output:**  
[]

---

### Example 3

**Input:**  
root = [1]

**Output:**  
[1]

---

## 💡 Intuition Behind the Approach

👉 Preorder traversal means:

1. Start with the root.
2. Visit everything in the **left** subtree.
3. Then move to the **right** subtree.

There are **two common approaches**:

- **Recursive:** Simple, directly follow definition.
- **Iterative:** Use a stack to simulate recursion.

✅ Both work in `O(n)` time where `n` is the number of nodes.

---

## 📚 Algorithm Explanation

### Recursive Preorder:

1. If root is `null`, return.
2. Add `root.val` to result.
3. Recursively traverse left subtree.
4. Recursively traverse right subtree.

### Iterative Preorder:

1. Use a stack initialized with the root.
2. While stack not empty:
   - Pop top node.
   - Add its value to result.
   - Push right child, then left child (so left is processed first).

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
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> result;
        preorder(root, result);
        return result;
    }
private:
    void preorder(TreeNode* node, vector<int>& res) {
        if (!node) return;
        res.push_back(node->val);
        preorder(node->left, res);
        preorder(node->right, res);
    }
};

// Driver code
int main() {
    TreeNode* root = new TreeNode(1);
    root->right = new TreeNode(2);
    root->right->left = new TreeNode(3);

    Solution sol;
    vector<int> ans = sol.preorderTraversal(root);
    cout << "Preorder Traversal: ";
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
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        preorder(root, res);
        return res;
    }
    private void preorder(TreeNode node, List<Integer> res) {
        if (node == null) return;
        res.add(node.val);
        preorder(node.left, res);
        preorder(node.right, res);
    }
}

public class Main {
    public static void main(String[] args) {
        TreeNode root = new TreeNode(1);
        root.right = new TreeNode(2);
        root.right.left = new TreeNode(3);

        Solution sol = new Solution();
        System.out.println("Preorder Traversal: " + sol.preorderTraversal(root));
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
    def preorderTraversal(self, root):
        res = []
        def preorder(node):
            if not node: return
            res.append(node.val)
            preorder(node.left)
            preorder(node.right)
        preorder(root)
        return res

# Driver
if __name__ == "__main__":
    root = TreeNode(1)
    root.right = TreeNode(2)
    root.right.left = TreeNode(3)
    sol = Solution()
    print("Preorder Traversal:", sol.preorderTraversal(root))


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
  preorderTraversal(root) {
    const res = [];
    function preorder(node) {
      if (!node) return;
      res.push(node.val);
      preorder(node.left);
      preorder(node.right);
    }
    preorder(root);
    return res;
  }
}

// Driver
let root = new TreeNode(1);
root.right = new TreeNode(2);
root.right.left = new TreeNode(3);

const sol = new Solution();
console.log("Preorder Traversal:", sol.preorderTraversal(root));
```

---

## 🧪 Tests You Can Try

Input: root = [1,null,2,3]
Output: [1,2,3]

Input: root = []
Output: []

Input: root = [1]
Output: [1]

Input: root = [1,2,3,4,5]
Output: [1,2,4,5,3]

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
