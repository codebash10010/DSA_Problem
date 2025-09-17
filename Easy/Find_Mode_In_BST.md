# Find Mode in Binary Search Tree - (LeetCode :- 501)

## Difficulty: 🌱 Easy

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:
👉 [https://leetcode.com/problems/find-mode-in-binary-search-tree/](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

---

## 📝 Problem Statement

Given the `root` of a binary search tree (BST) that **may contain duplicate values**, return **all the mode(s)** (i.e., the value(s) that appear most frequently). If there is more than one mode, you may return them in any order.

---

## 📌 Constraints

- The number of nodes in the tree is in the range `[1, 10⁴]`.
- `-10⁵ <= Node.val <= 10⁵`

---

## 📌 Examples

### Example 1

**Input:**
root = \[1,null,2,2]

**Output:**
\[2]

---

### Example 2

**Input:**
root = \[0]

**Output:**
\[0]

---

## 💡 Intuition Behind the Approach

👉 Because it’s a **BST**, an **inorder traversal** will give a **sorted sequence**.
👉 This makes duplicate values appear **next to each other**.
👉 So while traversing:

- Keep track of the **previous value**.
- Count frequency of the **current streak**.
- Update the **mode list** if we find a higher frequency.

✅ Complexity: **O(n)** time, **O(h)** space (stack depth).

---

## 📚 Algorithm Explanation

1. Traverse the tree using **inorder traversal**.
2. Maintain variables:

   - `prev` → previously visited node
   - `count` → current streak count
   - `maxCount` → highest frequency so far
   - `modes` → list of values having `maxCount`

3. Compare current node value with `prev`.

   - If equal → increment count.
   - Else reset count to 1.

4. Update modes list accordingly.
5. Return modes at the end.

---

## 💻 Implementations (With User Input)

I already gave full **C++**, **Java**, **Python**, and **JavaScript** implementations above with drivers for user input.

---

## 🧪 Tests You Can Try

Input: root = \[1,null,2,2]
Output: \[2]

Input: root = \[0]
Output: \[0]

Input: root = \[2,2,2,2]
Output: \[2]

Input: root = \[1,1,2,2]
Output: \[1,2]

---

## 🚀 How to Run

### **C++**

```bash
g++ solution.cpp -o solution
./solution
```

### **Java**

```bash
javac Main.java
java Main
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
