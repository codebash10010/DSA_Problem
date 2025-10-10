# Number of Good Leaf Nodes Pairs - (LeetCode :- 1530)

## 🏢 Companies Asked :- Amazon , Microsoft , Google , Meta  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

**Difficulty:** 🟠 Medium  

[🔗 Problem Link] (https://leetcode.com/problems/number-of-good-leaf-nodes-pairs/description/)

---

## 📝 Problem Statement

You are given the root of a binary tree and an integer `distance`.  

A pair of **two different leaf nodes** of a binary tree is said to be **good** if the length of the shortest path between them is **less than or equal to `distance`**.  

Return the number of good leaf node pairs in the tree.  

---

## 📌 Constraints
- The number of nodes in the tree is in the range `[1, 2 * 10⁴]`.  
- `1 <= Node.val <= 100`  
- `1 <= distance <= 10`  

---

## 📌 Examples

### Example 1
**Input:**  
`root = [1,2,3,null,4], distance = 3`  

**Output:**  
`1`  

**Explanation:**  
The leaf nodes are 4 and 3, and the distance between them is 3.

---

### Example 2
**Input:**  
`root = [1,2,3,4,5,6,7], distance = 3`  

**Output:**  
`2`

---

### Example 3
**Input:**  
`root = [7,1,4,6,null,5,3,null,null,null,null,null,2], distance = 3`  

**Output:**  
`1`  

---

## 💡 Intuition Behind the Approach

We need to count **pairs of leaf nodes** whose path length is ≤ `distance`.  

👉 Observations:  
1. The path between two leaf nodes goes **up to their Lowest Common Ancestor (LCA)**.  
2. If we know the distances of leaves in left and right subtrees of a node, we can **combine them** to count valid pairs.  

👉 Approach (DFS - Postorder):  
1. Perform a DFS.  
2. For each node:  
   - Get distances of leaf nodes in the left subtree.  
   - Get distances of leaf nodes in the right subtree.  
   - Count cross-pairs where `leftDist + rightDist <= distance`.  
3. Return an array of distances from this node to its leaves.  

---

## ⏱ Complexity Analysis
- **Time Complexity:** `O(n * d²)` (each node combines distances up to `d`)  
- **Space Complexity:** `O(n)` recursion stack  

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
using namespace std;

struct TreeNode {
    int val;
    TreeNode *left, *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

class Solution {
    int result = 0;
public:
    vector<int> dfs(TreeNode* root, int distance) {
        if (!root) return {};
        if (!root->left && !root->right) return {1}; // leaf
        
        auto left = dfs(root->left, distance);
        auto right = dfs(root->right, distance);
        
        for (int l : left) {
            for (int r : right) {
                if (l + r <= distance) result++;
            }
        }
        
        vector<int> dist;
        for (int l : left) if (l + 1 <= distance) dist.push_back(l + 1);
        for (int r : right) if (r + 1 <= distance) dist.push_back(r + 1);
        return dist;
    }
    
    int countPairs(TreeNode* root, int distance) {
        dfs(root, distance);
        return result;
    }
};
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
    int result = 0;
    
    public List<Integer> dfs(TreeNode root, int distance) {
        if (root == null) return new ArrayList<>();
        if (root.left == null && root.right == null) return Arrays.asList(1);
        
        List<Integer> left = dfs(root.left, distance);
        List<Integer> right = dfs(root.right, distance);
        
        for (int l : left) {
            for (int r : right) {
                if (l + r <= distance) result++;
            }
        }
        
        List<Integer> dist = new ArrayList<>();
        for (int l : left) if (l + 1 <= distance) dist.add(l + 1);
        for (int r : right) if (r + 1 <= distance) dist.add(r + 1);
        return dist;
    }
    
    public int countPairs(TreeNode root, int distance) {
        dfs(root, distance);
        return result;
    }
}
```

---

### **Python**

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    def countPairs(self, root: TreeNode, distance: int) -> int:
        self.result = 0
        
        def dfs(node):
            if not node:
                return []
            if not node.left and not node.right:
                return [1]
            
            left = dfs(node.left)
            right = dfs(node.right)
            
            for l in left:
                for r in right:
                    if l + r <= distance:
                        self.result += 1
            
            return [d + 1 for d in left + right if d + 1 <= distance]
        
        dfs(root)
        return self.result
```

---

### **JavaScript**

```javascript
class TreeNode {
    constructor(val, left = null, right = null) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

class Solution {
    constructor() {
        this.result = 0;
    }

    dfs(node, distance) {
        if (!node) return [];
        if (!node.left && !node.right) return [1];
        
        let left = this.dfs(node.left, distance);
        let right = this.dfs(node.right, distance);
        
        for (let l of left) {
            for (let r of right) {
                if (l + r <= distance) this.result++;
            }
        }
        
        let dist = [];
        for (let l of left) if (l + 1 <= distance) dist.push(l + 1);
        for (let r of right) if (r + 1 <= distance) dist.push(r + 1);
        return dist;
    }

    countPairs(root, distance) {
        this.dfs(root, distance);
        return this.result;
    }
}
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




