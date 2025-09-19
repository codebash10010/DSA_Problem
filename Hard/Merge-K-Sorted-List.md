# Merge k Sorted Lists - (LeetCode :- 23)

## Difficulty: 🔴 Hard

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:
👉 [https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)

---

## 📝 Problem Statement

You are given an array of `k` linked-lists, each sorted in ascending order.
Merge all the linked-lists into **one sorted linked-list** and return it.

---

## 📌 Constraints

- `k == lists.length`
- `0 <= k <= 10⁴`
- `0 <= lists[i].length <= 500`
- `-10⁴ <= lists[i][j] <= 10⁴`

---

## 📌 Examples

### Example 1

**Input:**
lists = \[\[1,4,5],\[1,3,4],\[2,6]]

**Output:**
\[1,1,2,3,4,4,5,6]

**Explanation:**
The linked-lists are:

```
1 -> 4 -> 5
1 -> 3 -> 4
2 -> 6
```

Merged → `1 -> 1 -> 2 -> 3 -> 4 -> 4 -> 5 -> 6`

---

### Example 2

**Input:**
lists = \[]

**Output:**
\[]

---

### Example 3

**Input:**
lists = \[\[]]

**Output:**
\[]

---

## 💡 Intuition Behind the Approach

We want to merge `k` sorted lists efficiently:

- **Brute Force**: Collect all nodes into an array, sort them, then rebuild a list.
  ❌ Complexity: `O(N log N)` where `N` is total nodes.

- **Sequential Merge**: Merge two lists at a time, repeatedly.
  ❌ Complexity: `O(kN)` (slow when `k` is large).

- **Optimal (Min-Heap/Priority Queue)** ✅

  - Put the **head of each list** into a min-heap (priority queue).
  - Repeatedly extract the minimum node, add it to the result list.
  - If that node has a next, push it into the heap.
  - Continue until heap is empty.
  - Complexity: `O(N log k)` (efficient).

---

## 📚 Algorithm Explanation

1. Use a **priority queue (min-heap)** based on node values.
2. Push the **head node of each list** into the heap.
3. While heap is not empty:

   - Pop the smallest node.
   - Add it to the merged list.
   - If it has a next node, push that into the heap.

4. Return the merged list’s head.

---

## 💻 Implementations

---

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x) : val(x), next(NULL) {}
};

struct Compare {
    bool operator()(ListNode* a, ListNode* b) {
        return a->val > b->val;
    }
};

class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        priority_queue<ListNode*, vector<ListNode*>, Compare> pq;
        for (auto node : lists) {
            if (node) pq.push(node);
        }
        ListNode dummy(0);
        ListNode* tail = &dummy;

        while (!pq.empty()) {
            ListNode* node = pq.top(); pq.pop();
            tail->next = node;
            tail = tail->next;
            if (node->next) pq.push(node->next);
        }
        return dummy.next;
    }
};

// Driver code
int main() {
    int k;
    cout << "Enter number of linked lists: ";
    cin >> k;
    vector<ListNode*> lists;
    for (int i = 0; i < k; i++) {
        int n; cout << "Enter size of list " << i+1 << ": ";
        cin >> n;
        ListNode* head = NULL, *tail = NULL;
        cout << "Enter elements: ";
        for (int j = 0; j < n; j++) {
            int x; cin >> x;
            if (!head) head = tail = new ListNode(x);
            else { tail->next = new ListNode(x); tail = tail->next; }
        }
        lists.push_back(head);
    }
    Solution sol;
    ListNode* result = sol.mergeKLists(lists);
    cout << "Merged List: ";
    while (result) {
        cout << result->val << " ";
        result = result->next;
    }
}
```

---

### **Java**

```java
import java.util.*;

class ListNode {
    int val;
    ListNode next;
    ListNode(int x) { val = x; }
}

class Solution {
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
        for (ListNode node : lists) {
            if (node != null) pq.add(node);
        }
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            tail.next = node;
            tail = tail.next;
            if (node.next != null) pq.add(node.next);
        }
        return dummy.next;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of linked lists: ");
        int k = sc.nextInt();
        ListNode[] lists = new ListNode[k];
        for (int i = 0; i < k; i++) {
            System.out.print("Enter size of list " + (i+1) + ": ");
            int n = sc.nextInt();
            ListNode head = null, tail = null;
            System.out.print("Enter elements: ");
            for (int j = 0; j < n; j++) {
                int x = sc.nextInt();
                if (head == null) head = tail = new ListNode(x);
                else { tail.next = new ListNode(x); tail = tail.next; }
            }
            lists[i] = head;
        }
        Solution sol = new Solution();
        ListNode result = sol.mergeKLists(lists);
        System.out.print("Merged List: ");
        while (result != null) {
            System.out.print(result.val + " ");
            result = result.next;
        }
    }
}
```

---

### **Python**

```python
import heapq

class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeKLists(self, lists):
        pq = []
        for idx, node in enumerate(lists):
            if node:
                heapq.heappush(pq, (node.val, idx, node))
        dummy = ListNode(0)
        tail = dummy
        while pq:
            val, idx, node = heapq.heappop(pq)
            tail.next = node
            tail = tail.next
            if node.next:
                heapq.heappush(pq, (node.next.val, idx, node.next))
        return dummy.next

# Driver
def build_list(arr):
    head = cur = None
    for x in arr:
        if not head:
            head = cur = ListNode(x)
        else:
            cur.next = ListNode(x)
            cur = cur.next
    return head

def print_list(head):
    while head:
        print(head.val, end=" ")
        head = head.next
    print()

if __name__ == "__main__":
    k = int(input("Enter number of linked lists: "))
    lists = []
    for i in range(k):
        n = int(input(f"Enter size of list {i+1}: "))
        arr = list(map(int, input("Enter elements: ").split()))
        lists.append(build_list(arr))
    sol = Solution()
    result = sol.mergeKLists(lists)
    print("Merged List:", end=" ")
    print_list(result)
```

---

### **JavaScript**

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

class ListNode {
  constructor(val) {
    this.val = val;
    this.next = null;
  }
}

class MinHeap {
  constructor() {
    this.data = [];
  }
  push(node) {
    this.data.push(node);
    this.data.sort((a, b) => a.val - b.val);
  }
  pop() {
    return this.data.shift();
  }
  isEmpty() {
    return this.data.length === 0;
  }
}

class Solution {
  mergeKLists(lists) {
    const pq = new MinHeap();
    for (let node of lists) if (node) pq.push(node);
    let dummy = new ListNode(0),
      tail = dummy;
    while (!pq.isEmpty()) {
      let node = pq.pop();
      tail.next = node;
      tail = tail.next;
      if (node.next) pq.push(node.next);
    }
    return dummy.next;
  }
}

function buildList(arr) {
  let head = null,
    cur = null;
  for (let x of arr) {
    if (!head) head = cur = new ListNode(x);
    else {
      cur.next = new ListNode(x);
      cur = cur.next;
    }
  }
  return head;
}

function printList(head) {
  let res = [];
  while (head) {
    res.push(head.val);
    head = head.next;
  }
  console.log(res.join(" "));
}

readline.question("Enter number of linked lists: ", (kStr) => {
  let k = parseInt(kStr);
  let lists = [];
  function readList(i) {
    if (i >= k) {
      const sol = new Solution();
      let result = sol.mergeKLists(lists);
      console.log("Merged List:");
      printList(result);
      readline.close();
      return;
    }
    readline.question(`Enter size of list ${i + 1}: `, (nStr) => {
      readline.question("Enter elements: ", (arrStr) => {
        let arr = arrStr.trim().split(" ").map(Number);
        lists.push(buildList(arr));
        readList(i + 1);
      });
    });
  }
  readList(0);
});
```

---

## 🧪 Tests You Can Try

**Input 1:**
lists = \[\[1,4,5],\[1,3,4],\[2,6]]
**Output:**
\[1,1,2,3,4,4,5,6]

**Input 2:**
lists = \[]
**Output:**
\[]

**Input 3:**
lists = \[\[]]
**Output:**
\[]

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
