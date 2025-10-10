# Reverse Linked List II - (LeetCode :- 92)

## Difficulty: 🔴 Medium

---

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

👉 [Problem Link] (https://leetcode.com/problems/reverse-linked-list-ii/)

---

## 📝 Problem Statement

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, **reverse the nodes of the list from position `left` to position `right`**, and return the modified list.

---

## 📌 Constraints

- The number of nodes in the list is `n`.
- `1 <= n <= 500`
- `-500 <= Node.val <= 500`
- `1 <= left <= right <= n`

---

## 📌 Examples

### Example 1

**Input:**
head = `[1,2,3,4,5]`, left = 2, right = 4

**Output:**
`[1,4,3,2,5]`

**Explanation:**
The sublist `[2,3,4]` is reversed to `[4,3,2]`.

---

### Example 2

**Input:**
head = `[5]`, left = 1, right = 1

**Output:**
`[5]`

**Explanation:**
Only one node, no change needed.

---

## 💡 Intuition Behind the Approach

1. **Skip the first `left-1` nodes** to reach the node before reversal starts.
2. **Reverse the sublist from `left` to `right`** using standard linked list reversal.
3. **Reconnect the reversed sublist** to the remaining list.

✅ The key is **pointer manipulation** without losing track of nodes.

---

## 📚 Algorithm Steps

1. Use a dummy node pointing to the head to simplify edge cases.
2. Move a pointer `prev` to the node **before `left`**.
3. Reverse the sublist from `left` to `right`.
4. Connect the `prev.next` to the new head of the reversed sublist.
5. Connect the tail of the reversed sublist to the node after `right`.

---

## 📊 Diagram

```
Before reversal (left=2, right=4):
1 -> 2 -> 3 -> 4 -> 5

Step 1: prev points to 1 (node before reversal)
Step 2: Reverse 2->3->4
Result:
1 -> 4 -> 3 -> 2 -> 5
```

---

## 💻 Implementations

### **C++**

```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(nullptr) {}
};

class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        if (!head || left == right) return head;

        ListNode dummy(0);
        dummy.next = head;
        ListNode* prev = &dummy;

        for (int i = 1; i < left; ++i)
            prev = prev->next;

        ListNode* curr = prev->next;
        for (int i = 0; i < right - left; ++i) {
            ListNode* temp = curr->next;
            curr->next = temp->next;
            temp->next = prev->next;
            prev->next = temp;
        }

        return dummy.next;
    }
};

// Driver
int main() {
    ListNode* head = new ListNode(1);
    head->next = new ListNode(2);
    head->next->next = new ListNode(3);
    head->next->next->next = new ListNode(4);
    head->next->next->next->next = new ListNode(5);

    int left = 2, right = 4;

    Solution sol;
    ListNode* newHead = sol.reverseBetween(head, left, right);

    while (newHead) {
        cout << newHead->val << " ";
        newHead = newHead->next;
    }
}
```

---

### **Java**

```java
class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; next = null; }
}

class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null || left == right) return head;

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;

        for (int i = 1; i < left; i++) prev = prev.next;

        ListNode curr = prev.next;
        for (int i = 0; i < right - left; i++) {
            ListNode temp = curr.next;
            curr.next = temp.next;
            temp.next = prev.next;
            prev.next = temp;
        }

        return dummy.next;
    }
}
```

---

### **Python**

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseBetween(self, head, left: int, right: int):
        if not head or left == right:
            return head

        dummy = ListNode(0)
        dummy.next = head
        prev = dummy

        for _ in range(left - 1):
            prev = prev.next

        curr = prev.next
        for _ in range(right - left):
            temp = curr.next
            curr.next = temp.next
            temp.next = prev.next
            prev.next = temp

        return dummy.next
```

---

### **JavaScript**

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

var reverseBetween = function (head, left, right) {
  if (!head || left === right) return head;

  let dummy = new ListNode(0);
  dummy.next = head;
  let prev = dummy;

  for (let i = 1; i < left; i++) prev = prev.next;

  let curr = prev.next;
  for (let i = 0; i < right - left; i++) {
    let temp = curr.next;
    curr.next = temp.next;
    temp.next = prev.next;
    prev.next = temp;
  }

  return dummy.next;
};
```

---

## 🧪 Example Test Cases

**Input:**
head = `[1,2,3,4,5]`, left = 2, right = 4
**Output:**
`[1,4,3,2,5]`

**Input:**
head = `[5]`, left = 1, right = 1
**Output:**
`[5]`

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
