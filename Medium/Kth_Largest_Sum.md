# 2583. Kth Largest Sum in a Binary Tree
## 🏢 Companies Asked:- Amazon, Google, Microsoft, Meta
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)
---

## 🔗 Problem Link
You can find the original problem here:  

👉 https://leetcode.com/problems/adding-spaces-to-a-string/](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/description/

---

## Problem Statement

You are given the root of a binary tree and a positive integer `k`.

The **level sum** in the tree is the sum of the values of the nodes that are on the same level.

Return the `k`th largest level sum in the tree (not necessarily distinct). If there are fewer than `k` levels in the tree, return `-1`.

> Note that two nodes are on the same level if they have the same distance from the root.

## Examples

**Example 1:**

```
Input: root = [5,8,9,2,1,3,7,4,6], k = 2
Output: 13
```

**Example 2:**

```
Input: root = [1,2,null,3], k = 1
Output: 3
```

## Constraints

* The number of nodes in the tree is `n`.
* `2 <= n <= 10^5`
* `1 <= Node.val <= 10^6`
* `1 <= k <= n`

### Intuition

To solve this problem efficiently, we can use a level-order traversal (BFS) because it allows us to process nodes level by level:

Traverse the tree using a queue.

For each level, calculate the sum of all nodes at that level.

Store these sums in a list.

Sort the list of sums in descending order and return the k-th largest.

This approach guarantees that each node is visited exactly once, and we only need to sort the sums of levels, which is much smaller than the total number of nodes.

## Approach

1. Level Order Traversal (BFS) to compute sums per level.
2. Store sums and sort them to find k-th largest.

## Python Solution

```python
from collections import deque

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def kthLargestLevelSum(root: TreeNode, k: int) -> int:
    if not root:
        return -1

    queue = deque([root])
    level_sums = []

    while queue:
        level_size = len(queue)
        level_sum = 0
        for _ in range(level_size):
            node = queue.popleft()
            level_sum += node.val
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
        level_sums.append(level_sum)

    level_sums.sort(reverse=True)
    return level_sums[k-1] if k <= len(level_sums) else -1

# Driver Code
if __name__ == '__main__':
    n = int(input("Enter number of nodes: "))
    nodes = list(map(int, input(f"Enter {n} node values: ").split()))
    k = int(input("Enter k: "))
    
    # Create simple binary tree from list for demo purposes
    tree_nodes = [TreeNode(val) for val in nodes]
    for i in range(n):
        if 2*i + 1 < n:
            tree_nodes[i].left = tree_nodes[2*i + 1]
        if 2*i + 2 < n:
            tree_nodes[i].right = tree_nodes[2*i + 2]
    root = tree_nodes[0]
    print(kthLargestLevelSum(root, k))
```

## C++ Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

struct TreeNode {
    int val;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

int kthLargestLevelSum(TreeNode* root, int k) {
    if (!root) return -1;
    queue<TreeNode*> q;
    q.push(root);
    vector<long long> sums;
    while (!q.empty()) {
        int sz = q.size();
        long long level_sum = 0;
        for (int i = 0; i < sz; ++i) {
            TreeNode* node = q.front(); q.pop();
            level_sum += node->val;
            if (node->left) q.push(node->left);
            if (node->right) q.push(node->right);
        }
        sums.push_back(level_sum);
    }
    sort(sums.rbegin(), sums.rend());
    return k <= sums.size() ? sums[k-1] : -1;
}

int main() {
    int n, k;
    cout << "Enter number of nodes: "; cin >> n;
    vector<int> vals(n);
    cout << "Enter node values: ";
    for (int i = 0; i < n; ++i) cin >> vals[i];
    cout << "Enter k: "; cin >> k;

    vector<TreeNode*> nodes(n);
    for (int i = 0; i < n; ++i) nodes[i] = new TreeNode(vals[i]);
    for (int i = 0; i < n; ++i) {
        if (2*i+1 < n) nodes[i]->left = nodes[2*i+1];
        if (2*i+2 < n) nodes[i]->right = nodes[2*i+2];
    }

    cout << kthLargestLevelSum(nodes[0], k) << endl;
    return 0;
}
```

## Java Solution

```java
import java.util.*;

class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class KthLargestLevelSum {
    public static int kthLargestLevelSum(TreeNode root, int k) {
        if (root == null) return -1;
        Queue<TreeNode> q = new LinkedList<>();
        q.add(root);
        List<Long> sums = new ArrayList<>();

        while (!q.isEmpty()) {
            int sz = q.size();
            long levelSum = 0;
            for (int i = 0; i < sz; i++) {
                TreeNode node = q.poll();
                levelSum += node.val;
                if (node.left != null) q.add(node.left);
                if (node.right != null) q.add(node.right);
            }
            sums.add(levelSum);
        }

        sums.sort(Collections.reverseOrder());
        return k <= sums.size() ? sums.get(k-1).intValue() : -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of nodes: ");
        int n = sc.nextInt();
        int[] vals = new int[n];
        System.out.print("Enter node values: ");
        for (int i = 0; i < n; i++) vals[i] = sc.nextInt();
        System.out.print("Enter k: ");
        int k = sc.nextInt();

        TreeNode[] nodes = new TreeNode[n];
        for (int i = 0; i < n; i++) nodes[i] = new TreeNode(vals[i]);
        for (int i = 0; i < n; i++) {
            if (2*i + 1 < n) nodes[i].left = nodes[2*i + 1];
            if (2*i + 2 < n) nodes[i].right = nodes[2*i + 2];
        }
        System.out.println(kthLargestLevelSum(nodes[0], k));
    }
}
```

## JavaScript Solution

```javascript
class TreeNode {
    constructor(val) {
        this.val = val;
        this.left = null;
        this.right = null;
    }
}

function kthLargestLevelSum(root, k) {
    if (!root) return -1;
    let queue = [root];
    let sums = [];

    while (queue.length > 0) {
        let sz = queue.length;
        let levelSum = 0;
        for (let i = 0; i < sz; i++) {
            let node = queue.shift();
            levelSum += node.val;
            if (node.left) queue.push(node.left);
            if (node.right) queue.push(node.right);
        }
        sums.push(levelSum);
    }

    sums.sort((a,b) => b-a);
    return k <= sums.length ? sums[k-1] : -1;
}

// Driver code using Node.js readline
const readline = require('readline');
const rl = readline.createInterface({ input: process.stdin, output: process.stdout });

rl.question('Enter number of nodes: ', n => {
    rl.question(`Enter ${n} node values: `, vals => {
        let values = vals.split(' ').map(Number);
        rl.question('Enter k: ', k => {
            let nodes = values.map(v => new TreeNode(v));
            for (let i = 0; i < values.length; i++) {
                if (2*i + 1 < values.length) nodes[i].left = nodes[2*i + 1];
                if (2*i + 2 < values.length) nodes[i].right = nodes[2*i + 2];
            }
            console.log(kthLargestLevelSum(nodes[0], parseInt(k)));
            rl.close();
        });
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




