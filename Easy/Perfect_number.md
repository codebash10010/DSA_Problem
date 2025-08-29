# Delete the Middle Node of a Linked List - (LeetCode :- 2095)
## Difficulty:  🌿 Easy  

## 🏢 Companies Asked :- Adobe 

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list/

---

## 📝 Problem Statement

You are given the `head` of a **linked list**.  
Delete the **middle node**, and return the head of the modified linked list.  

- The **middle node** of a linked list of size `n` is the `⌊n / 2⌋`th node from the start (0-indexed).  
- If the list has only **1 node**, deleting it will result in an **empty list**.

---

## 📌 Constraints
- The number of nodes in the list is in the range `[1, 10⁵]`
- `1 <= Node.val <= 10⁵`

---

## 📌 Examples

### **Example 1**
**Input:**  
head = [1,3,4,7,1,2,6]

**Output:**  
[1,3,4,1,2,6]

**Explanation:**  
- Size `n = 7` → middle index = `⌊7/2⌋ = 3`  
- Delete node at index 3 → value `7`.  

Final List → `[1,3,4,1,2,6]`.

---

### **Example 2**
**Input:**  
head = [1,2,3,4]

**Output:**  
[1,2,4]

**Explanation:**  
- Size `n = 4` → middle index = `⌊4/2⌋ = 2`  
- Delete node at index 2 → value `3`.  

Final List → `[1,2,4]`.

---

### **Example 3**
**Input:**  
head = [2,1]

**Output:**  
[2]


**Explanation:**  
- Size `n = 2` → middle index = `⌊2/2⌋ = 1`  
- Delete node at index 1 → value `1`.  

Final List → `[2]`.

---

## 💡 Intuition Behind the Approach

The problem is essentially about **removing the middle node**.  

Two common approaches:  

1. **Two-pass method (easy to implement):**  
   - First pass: Count the length `n`.  
   - Middle = `⌊n/2⌋`.  
   - Second pass: Traverse until node `middle - 1` and delete `middle`.  

2. **One-pass method (fast & optimal):**  
   - Use **slow and fast pointers**:  
     - `slow` moves one step, `fast` moves two steps.  
     - When `fast` reaches end, `slow` is at middle.  
   - Delete the `slow` node by skipping it.  

👉 Since only deletion of middle is required, **two-pointer method is optimal in O(n)** with a single traversal.

---

## 📚 Algorithm Explanation

- Initialize two pointers: `slow` and `fast`, and a `prev` to track node before `slow`.  
- Traverse:  
  - Move `slow` by 1 step, `fast` by 2 steps.  
  - When `fast` reaches end, `slow` will be at middle.  
- Delete the middle:  
  - `prev.next = slow.next`  

**Time Complexity:** `O(n)`  
**Space Complexity:** `O(1)`

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};

class Solution {
public:
    ListNode* deleteMiddle(ListNode* head) {
        if (!head || !head->next) return NULL; // only one node

        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* prev = NULL;

        while (fast && fast->next) {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }

        // delete middle
        prev->next = slow->next;
        return head;
    }
};

// Driver code
int main() {
    int n;
    cout << "Enter number of nodes: ";
    cin >> n;
    ListNode* head = NULL;
    ListNode* tail = NULL;
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) {
        int x; cin >> x;
        if (!head) {
            head = tail = new ListNode(x);
        } else {
            tail->next = new ListNode(x);
            tail = tail->next;
        }
    }

    Solution sol;
    head = sol.deleteMiddle(head);

    cout << "List after deletion: ";
    ListNode* cur = head;
    while (cur) {
        cout << cur->val << " ";
        cur = cur->next;
    }
}
```
---

### Java

```java
import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class Solution {
    public ListNode deleteMiddle(ListNode head) {
        if (head == null || head.next == null) return null;

        ListNode slow = head, fast = head, prev = null;
        while (fast != null && fast.next != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = slow.next; // delete middle
        return head;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of nodes: ");
        int n = sc.nextInt();
        ListNode head = null, tail = null;
        System.out.println("Enter elements: ");
        for (int i = 0; i < n; i++) {
            int x = sc.nextInt();
            if (head == null) {
                head = tail = new ListNode(x);
            } else {
                tail.next = new ListNode(x);
                tail = tail.next;
            }
        }
        Solution sol = new Solution();
        head = sol.deleteMiddle(head);

        System.out.print("List after deletion: ");
        ListNode cur = head;
        while (cur != null) {
            System.out.print(cur.val + " ");
            cur = cur.next;
        }
    }
}

```

---

### Python

```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def deleteMiddle(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return None

        slow, fast = head, head
        prev = None

        while fast and fast.next:
            prev = slow
            slow = slow.next
            fast = fast.next.next

        prev.next = slow.next
        return head

# Driver code
def build_list(arr):
    head = ListNode(arr[0])
    cur = head
    for x in arr[1:]:
        cur.next = ListNode(x)
        cur = cur.next
    return head

def print_list(head):
    cur = head
    while cur:
        print(cur.val, end=" ")
        cur = cur.next
    print()

if __name__ == "__main__":
    n = int(input("Enter number of nodes: "))
    arr = list(map(int, input("Enter elements: ").split()))
    head = build_list(arr)
    sol = Solution()
    head = sol.deleteMiddle(head)
    print("List after deletion:", end=" ")
    print_list(head)

```

---

### JavaScript 

```javascript
class ListNode {
    constructor(val) {
        this.val = val;
        this.next = null;
    }
}

class Solution {
    deleteMiddle(head) {
        if (!head || !head.next) return null;

        let slow = head, fast = head, prev = null;
        while (fast && fast.next) {
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
        }
        prev.next = slow.next;
        return head;
    }
}

// Driver
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

function buildList(arr) {
    let head = new ListNode(arr[0]);
    let cur = head;
    for (let i = 1; i < arr.length; i++) {
        cur.next = new ListNode(arr[i]);
        cur = cur.next;
    }
    return head;
}

function printList(head) {
    let cur = head;
    let res = [];
    while (cur) {
        res.push(cur.val);
        cur = cur.next;
    }
    console.log(res.join(" "));
}

readline.question("Enter number of nodes: ", (nStr) => {
    readline.question("Enter elements: ", (arrStr) => {
        const arr = arrStr.trim().split(" ").map(Number);
        let head = buildList(arr);
        const sol = new Solution();
        head = sol.deleteMiddle(head);
        console.log("List after deletion:");
        printList(head);
        readline.close();
    });
});

```

---

## 🧪 Tests You Can Try

Input: 28
Output: true

Input: 12
Output: false

Input: 6
Output: true

Input: 496
Output: true

Input: 25
Output: false

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

