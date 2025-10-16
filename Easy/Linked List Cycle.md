# Linked List Cycle - (LeetCode :- 141)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Facebook, Adobe

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟢 Easy

[🔗 Problem Link](https://leetcode.com/problems/linked-list-cycle/)

---

## 🧩 Problem Statement

Given the `head` of a linked list, determine if the linked list has a **cycle** in it.

A **cycle** exists if there is a node in the list that can be reached again by continuously following the `next` pointer.

Return `true` if there is a cycle in the linked list. Otherwise, return `false`.

---

## 📌 Constraints

* The number of nodes in the list is in the range `[0, 10^4]`.
* `-10^5 <= Node.val <= 10^5`
* `pos` is the index of the node that tail connects to. `pos == -1` means no cycle.

---

## 📌 Example

### Example 1

Input:

```
head = [3,2,0,-4], pos = 1
```

Output:

```
true
```

Explanation: The tail connects to the 1st node, forming a cycle.

### Example 2

Input:

```
head = [1,2], pos = 0
```

Output:

```
true
```

---

### Example 3

Input:

```
head = [1], pos = -1
```

Output:

```
false
```

---

## 💡 Intuition

Use **Floyd’s Cycle Detection (Tortoise and Hare)**:

* Two pointers, `slow` and `fast`.
* `slow` moves 1 step at a time, `fast` moves 2 steps.
* If `fast` meets `slow`, a cycle exists.
* If `fast` reaches `NULL`, no cycle.

---

## ⚙️ Approach (Step-by-Step)

1. Initialize `slow = head`, `fast = head`.
2. While `fast` and `fast.next` are not `NULL`:

   * Move `slow = slow.next`
   * Move `fast = fast.next.next`
   * If `slow == fast`, return `true`
3. Return `false`

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

struct ListNode{
    int val;
    ListNode* next;
    ListNode(int x): val(x), next(NULL){}
};

bool hasCycle(ListNode *head){
    ListNode *slow=head, *fast=head;
    while(fast && fast->next){
        slow = slow->next;
        fast = fast->next->next;
        if(slow==fast) return true;
    }
    return false;
}

int main(){
    int n;
    cin >> n;
    vector<int> vals(n);
    for(int i=0;i<n;i++) cin >> vals[i];
    int pos; 
    cin >> pos;

    vector<ListNode*> nodes(n);
    for(int i=0;i<n;i++) nodes[i] = new ListNode(vals[i]);
    for(int i=0;i<n-1;i++) nodes[i]->next = nodes[i+1];
    if(pos!=-1) nodes[n-1]->next = nodes[pos];

    cout << (hasCycle(nodes[0]) ? "true" : "false") << endl;
}
```

### ☕ Java

```java
import java.util.*;

class ListNode{
    int val;
    ListNode next;
    ListNode(int val){ this.val=val; this.next=null; }
}

public class Main{
    public static boolean hasCycle(ListNode head){
        ListNode slow=head, fast=head;
        while(fast!=null && fast.next!=null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow==fast) return true;
        }
        return false;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        ListNode[] nodes = new ListNode[n];
        for(int i=0;i<n;i++) nodes[i] = new ListNode(sc.nextInt());
        int pos = sc.nextInt();

        for(int i=0;i<n-1;i++) nodes[i].next = nodes[i+1];
        if(pos!=-1) nodes[n-1].next = nodes[pos];

        System.out.println(hasCycle(nodes[0]));
        sc.close();
    }
}
```

### 🐍 Python

```python
class ListNode:
    def __init__(self, val=0):
        self.val = val
        self.next = None

def hasCycle(head):
    slow, fast = head, head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow==fast:
            return True
    return False

if __name__=="__main__":
    n=int(input())
    vals=list(map(int,input().split()))
    pos=int(input())
    nodes=[ListNode(v) for v in vals]
    for i in range(n-1):
        nodes[i].next = nodes[i+1]
    if pos!=-1:
        nodes[-1].next = nodes[pos]
    print(hasCycle(nodes[0]))
```

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout
});

class ListNode{
    constructor(val){ this.val=val; this.next=null; }
}

function hasCycle(head){
    let slow=head, fast=head;
    while(fast && fast.next){
        slow = slow.next;
        fast = fast.next.next;
        if(slow===fast) return true;
    }
    return false;
}

readline.question("Enter n, values and pos: ", line=>{
    let parts=line.trim().split(" ").map(Number);
    let n=parts[0];
    let vals=parts.slice(1,n+1);
    let pos=parts[n+1];
    let nodes=vals.map(v=>new ListNode(v));
    for(let i=0;i<n-1;i++) nodes[i].next = nodes[i+1];
    if(pos!=-1) nodes[n-1].next = nodes[pos];
    console.log(hasCycle(nodes[0]));
    readline.close();
});
```

---

## ⏱ Complexity

* **Time:** O(n)
* **Space:** O(1)

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

### **JavaScript**

```bash
node solution.js
```

---
## 🙏 Thanks

Thanks for checking out this repository ❤️
If you found it helpful, don’t forget to ⭐ **star this repo** and share it with others! 🚀