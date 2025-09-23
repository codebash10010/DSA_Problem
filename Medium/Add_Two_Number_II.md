# Add Two Numbers II - (LeetCode :- 445)

## Difficulty: 🟠 Medium

---

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

👉 [Problem Link](https://leetcode.com/problems/add-two-numbers-ii/)

---

## 📝 Problem Statement

You are given **two non-empty linked lists** representing two non-negative integers.

- The **most significant digit comes first**.
- Each node contains a **single digit**.
- Add the two numbers and return the sum as a linked list.
- You may assume the two numbers do not contain any leading zero, except the number 0 itself.

---

## 📌 Examples

### Example 1

**Input:**
l1 = `[7,2,4,3]`, l2 = `[5,6,4]`

**Output:**
`[7,8,0,7]`

**Explanation:**
7243 + 564 = **7807**

---

### Example 2

**Input:**
l1 = `[2,4,3]`, l2 = `[5,6,4]`

**Output:**
`[8,0,7]`

**Explanation:**
243 + 564 = **807**

---

### Example 3

**Input:**
l1 = `[0]`, l2 = `[0]`

**Output:**
`[0]`

---

## 💡 Intuition

- Digits are in **forward order**, so we can’t just traverse like normal.
- Two common strategies:

  - **Use stacks** → push digits of both lists, pop to add from least significant digit.
  - **Reverse both lists**, add, then reverse back.

- Stack approach avoids modifying input lists.

---

## 📚 Algorithm Steps

1. Push all digits of `l1` and `l2` into two stacks.
2. While stacks are not empty (or carry exists):

   - Pop digits, add with carry.
   - Create a new node with `sum % 10`, link it to the result.

3. Return the head of the result.

---

## 💻 Implementations (with Driver Code)

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

class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        stack<int> s1, s2;
        while (l1) { s1.push(l1->val); l1 = l1->next; }
        while (l2) { s2.push(l2->val); l2 = l2->next; }

        int carry = 0;
        ListNode* head = nullptr;
        while (!s1.empty() || !s2.empty() || carry) {
            int sum = carry;
            if (!s1.empty()) { sum += s1.top(); s1.pop(); }
            if (!s2.empty()) { sum += s2.top(); s2.pop(); }
            carry = sum / 10;

            ListNode* node = new ListNode(sum % 10);
            node->next = head;
            head = node;
        }
        return head;
    }
};

// Helper: build linked list
ListNode* buildList(vector<int>& arr) {
    ListNode* head = nullptr;
    ListNode* tail = nullptr;
    for (int x : arr) {
        ListNode* node = new ListNode(x);
        if (!head) head = tail = node;
        else { tail->next = node; tail = node; }
    }
    return head;
}

// Helper: print linked list
void printList(ListNode* head) {
    while (head) {
        cout << head->val;
        if (head->next) cout << " -> ";
        head = head->next;
    }
    cout << endl;
}

int main() {
    int n, m;
    cout << "Enter size of first list: ";
    cin >> n;
    vector<int> arr1(n);
    cout << "Enter elements: ";
    for (int i = 0; i < n; i++) cin >> arr1[i];

    cout << "Enter size of second list: ";
    cin >> m;
    vector<int> arr2(m);
    cout << "Enter elements: ";
    for (int i = 0; i < m; i++) cin >> arr2[i];

    ListNode* l1 = buildList(arr1);
    ListNode* l2 = buildList(arr2);

    Solution sol;
    ListNode* res = sol.addTwoNumbers(l1, l2);

    cout << "Result: ";
    printList(res);
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
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        Stack<Integer> s1 = new Stack<>();
        Stack<Integer> s2 = new Stack<>();
        while (l1 != null) { s1.push(l1.val); l1 = l1.next; }
        while (l2 != null) { s2.push(l2.val); l2 = l2.next; }

        int carry = 0;
        ListNode head = null;
        while (!s1.isEmpty() || !s2.isEmpty() || carry != 0) {
            int sum = carry;
            if (!s1.isEmpty()) sum += s1.pop();
            if (!s2.isEmpty()) sum += s2.pop();
            carry = sum / 10;

            ListNode node = new ListNode(sum % 10);
            node.next = head;
            head = node;
        }
        return head;
    }
}

public class Main {
    static ListNode buildList(int[] arr) {
        ListNode head = null, tail = null;
        for (int x : arr) {
            ListNode node = new ListNode(x);
            if (head == null) head = tail = node;
            else { tail.next = node; tail = node; }
        }
        return head;
    }

    static void printList(ListNode head) {
        while (head != null) {
            System.out.print(head.val);
            if (head.next != null) System.out.print(" -> ");
            head = head.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter size of first list: ");
        int n = sc.nextInt();
        int[] arr1 = new int[n];
        System.out.println("Enter elements: ");
        for (int i = 0; i < n; i++) arr1[i] = sc.nextInt();

        System.out.print("Enter size of second list: ");
        int m = sc.nextInt();
        int[] arr2 = new int[m];
        System.out.println("Enter elements: ");
        for (int i = 0; i < m; i++) arr2[i] = sc.nextInt();

        ListNode l1 = buildList(arr1);
        ListNode l2 = buildList(arr2);

        Solution sol = new Solution();
        ListNode res = sol.addTwoNumbers(l1, l2);

        System.out.print("Result: ");
        printList(res);
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
    def addTwoNumbers(self, l1, l2):
        s1, s2 = [], []
        while l1:
            s1.append(l1.val)
            l1 = l1.next
        while l2:
            s2.append(l2.val)
            l2 = l2.next

        carry = 0
        head = None
        while s1 or s2 or carry:
            sum_val = carry
            if s1: sum_val += s1.pop()
            if s2: sum_val += s2.pop()
            carry = sum_val // 10
            node = ListNode(sum_val % 10)
            node.next = head
            head = node
        return head

# Helpers
def build_list(arr):
    head = tail = None
    for x in arr:
        node = ListNode(x)
        if not head:
            head = tail = node
        else:
            tail.next = node
            tail = node
    return head

def print_list(head):
    while head:
        print(head.val, end=" -> " if head.next else "")
        head = head.next
    print()

# Driver
if __name__ == "__main__":
    n = int(input("Enter size of first list: "))
    arr1 = list(map(int, input("Enter elements: ").split()))
    m = int(input("Enter size of second list: "))
    arr2 = list(map(int, input("Enter elements: ").split()))

    l1 = build_list(arr1)
    l2 = build_list(arr2)

    sol = Solution()
    res = sol.addTwoNumbers(l1, l2)

    print("Result:", end=" ")
    print_list(res)
```

---

### **JavaScript (Node.js)**

```javascript
class ListNode {
  constructor(val = 0, next = null) {
    this.val = val;
    this.next = next;
  }
}

class Solution {
  addTwoNumbers(l1, l2) {
    let s1 = [],
      s2 = [];
    while (l1) {
      s1.push(l1.val);
      l1 = l1.next;
    }
    while (l2) {
      s2.push(l2.val);
      l2 = l2.next;
    }

    let carry = 0,
      head = null;
    while (s1.length || s2.length || carry) {
      let sum = carry;
      if (s1.length) sum += s1.pop();
      if (s2.length) sum += s2.pop();
      carry = Math.floor(sum / 10);
      let node = new ListNode(sum % 10);
      node.next = head;
      head = node;
    }
    return head;
  }
}

// Helpers
function buildList(arr) {
  let head = null,
    tail = null;
  for (let x of arr) {
    let node = new ListNode(x);
    if (!head) head = tail = node;
    else {
      tail.next = node;
      tail = node;
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
  console.log(res.join(" -> "));
}

// Driver
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter size of first list: ", (nStr) => {
  readline.question("Enter elements: ", (arr1Str) => {
    let arr1 = arr1Str.trim().split(" ").map(Number);
    readline.question("Enter size of second list: ", (mStr) => {
      readline.question("Enter elements: ", (arr2Str) => {
        let arr2 = arr2Str.trim().split(" ").map(Number);

        let l1 = buildList(arr1);
        let l2 = buildList(arr2);

        let sol = new Solution();
        let res = sol.addTwoNumbers(l1, l2);

        process.stdout.write("Result: ");
        printList(res);
        readline.close();
      });
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
