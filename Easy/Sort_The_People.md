# Sort the People - (LeetCode :- 2418)

## Difficulty: 🌿 Easy

## 🏢 Companies Asked :- Amazon, Google, Microsoft

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)  
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

---

## 🔗 Problem Link

You can find the original problem here:  
👉 https://leetcode.com/problems/sort-the-people/

---

## 📝 Problem Statement

You are given:

- An array of **strings** `names`
- An array of **distinct positive integers** `heights`

Both arrays are of the same length `n`.

For each index `i`:

- `names[i]` = name of the i-th person
- `heights[i]` = height of the i-th person

Return `names` **sorted in descending order of heights**.

---

## 📌 Constraints

- `n == names.length == heights.length`
- `1 <= n <= 10⁵`
- `1 <= names[i].length <= 20`
- `1 <= heights[i] <= 10⁵`
- All `heights[i]` are distinct.
- `names[i]` consists of lowercase and uppercase English letters.

---

## 📌 Examples

### Example 1

**Input:**  
names = ["Mary","John","Emma"], heights = [180,165,170]

**Output:**  
["Mary","Emma","John"]

**Explanation:**

- Mary → 180
- John → 165
- Emma → 170

Sort by descending height → **Mary (180), Emma (170), John (165)**

---

### Example 2

**Input:**  
names = ["Alice","Bob","Bob"], heights = [155,185,150]

**Output:**  
["Bob","Alice","Bob"]

**Explanation:**

- Alice → 155
- Bob → 185
- Bob → 150

Sort → **Bob (185), Alice (155), Bob (150)**

---

## 💡 Intuition Behind the Approach

👉 The task is simply to **sort pairs of (name, height)** in **descending order of height**.

Steps:

1. Combine names and heights into pairs: `(height, name)`.
2. Sort the pairs by `height` (descending).
3. Extract only names from the sorted pairs.

✅ Sorting ensures people are arranged correctly.

**Time Complexity:** `O(n log n)` (sorting).  
**Space Complexity:** `O(n)` (storing pairs).

---

## 📚 Algorithm Explanation

1. Pair up `names[i]` with `heights[i]`.
2. Sort the pairs by height in descending order.
3. Extract and return the sorted `names`.

---

## 💻 Implementations

### **C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

class Solution {
public:
    vector<string> sortPeople(vector<string>& names, vector<int>& heights) {
        vector<pair<int, string>> people;
        for (int i = 0; i < names.size(); i++) {
            people.push_back({heights[i], names[i]});
        }
        sort(people.rbegin(), people.rend()); // sort by height descending
        vector<string> ans;
        for (auto& p : people) ans.push_back(p.second);
        return ans;
    }
};

// Driver code
int main() {
    int n;
    cout << "Enter number of people: ";
    cin >> n;
    vector<string> names(n);
    vector<int> heights(n);
    cout << "Enter names: ";
    for (int i = 0; i < n; i++) cin >> names[i];
    cout << "Enter heights: ";
    for (int i = 0; i < n; i++) cin >> heights[i];
    Solution sol;
    vector<string> result = sol.sortPeople(names, heights);
    cout << "Sorted people: ";
    for (string s : result) cout << s << " ";
}
```

---

### Java

```java
import java.util.*;

class Solution {
    public String[] sortPeople(String[] names, int[] heights) {
        int n = names.length;
        List<int[]> people = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            people.add(new int[]{heights[i], i});
        }
        people.sort((a, b) -> b[0] - a[0]); // sort descending by height
        String[] ans = new String[n];
        for (int i = 0; i < n; i++) {
            ans[i] = names[people.get(i)[1]];
        }
        return ans;
    }
}

// Driver
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        String[] names = new String[n];
        int[] heights = new int[n];
        for (int i = 0; i < n; i++) names[i] = sc.next();
        for (int i = 0; i < n; i++) heights[i] = sc.nextInt();
        Solution sol = new Solution();
        String[] result = sol.sortPeople(names, heights);
        System.out.println("Sorted people: " + String.join(" ", result));
    }
}


```

---

### Python

```python
class Solution:
    def sortPeople(self, names, heights):
        people = list(zip(heights, names))
        people.sort(reverse=True)
        return [name for _, name in people]

# Driver code
if __name__ == "__main__":
    n = int(input("Enter number of people: "))
    names = input("Enter names: ").split()
    heights = list(map(int, input("Enter heights: ").split()))
    sol = Solution()
    print("Sorted people:", sol.sortPeople(names, heights))


```

---

### JavaScript

```javascript
class Solution {
  sortPeople(names, heights) {
    let people = names.map((name, i) => [heights[i], name]);
    people.sort((a, b) => b[0] - a[0]);
    return people.map((p) => p[1]);
  }
}

// Driver
const readline = require("readline").createInterface({
  input: process.stdin,
  output: process.stdout,
});

readline.question("Enter number of people: ", (nStr) => {
  let n = parseInt(nStr);
  readline.question("Enter names: ", (namesStr) => {
    let names = namesStr.trim().split(" ");
    readline.question("Enter heights: ", (heightsStr) => {
      let heights = heightsStr.trim().split(" ").map(Number);
      const sol = new Solution();
      console.log("Sorted people:", sol.sortPeople(names, heights).join(" "));
      readline.close();
    });
  });
});
```

---

## 🧪 Tests You Can Try

Input:
names = ["Mary","John","Emma"]
heights = [180,165,170]

Output:
["Mary","Emma","John"]

Input:
names = ["Alice","Bob","Bob"]
heights = [155,185,150]

Output:
["Bob","Alice","Bob"]

Input:
names = ["Tom","Jerry","Mickey","Donald"]
heights = [170,160,180,175]

Output:
["Mickey","Donald","Tom","Jerry"]

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
