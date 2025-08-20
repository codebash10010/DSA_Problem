# Adding Spaces to a String - (LeetCode :- 2109)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Adobe, Bloomberg  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)

👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)
---

## 🔗 Problem Link
You can find the original problem here:  

👉 https://leetcode.com/problems/adding-spaces-to-a-string/

---

## 📝 Problem Statement

You are given a **0-indexed string** `s` and a **0-indexed integer array** `spaces` that describes the indices in the original string where spaces will be added.  

Each space should be inserted **before the character** at the given index.  

Return the modified string after the spaces have been added.

---

## 📌 Constraints
- `1 <= s.length <= 3 * 10⁵`
- `s` consists only of **lowercase and uppercase English letters**
- `1 <= spaces.length <= 3 * 10⁵`
- `0 <= spaces[i] <= s.length - 1`
- All `spaces[i]` are **strictly increasing**

---

## 📌 Examples

### **Example 1**

**Input:**  
s = "LeetcodeHelpsMeLearn"
spaces = [8,13,15]

**Output:**  
"Leetcode Helps Me Learn"

**Explanation:**  
Spaces are added before indices `8, 13, 15`.  

---

### **Example 2**

**Input:**  
s = "icodeinpython"
spaces = [1,5,7,9]

**Output:**  
"i code in py thon"

**Explanation:**  
Spaces are added before indices `1, 5, 7, 9`.

---

### **Example 3**

**Input:**  
s = "spacing"
spaces = [0,1,2,3,4,5,6]


**Output:**  
" s p a c i n g"



---

## 💡 Intuition Behind the Approach

✅ We need to insert spaces at specific indices.  
✅ Since indices are strictly increasing, we can **traverse the string once** while keeping track of where spaces go.  

👉 Idea:  
- Maintain a **set or pointer** for `spaces`.  
- While traversing the string:
  - If the current index is in `spaces`, add a `" "` before appending the character.
  - Otherwise, just append the character.

This gives us the required result efficiently.

🔑 **Key Insight:** Instead of inserting into the string repeatedly (which is costly), we **build the new string in one pass**.

---

## 📚 Algorithm Explanation

1. Initialize an empty `StringBuilder` (or list in Python, or array in JS).  
2. Use a pointer `j` to track the current position in `spaces`.  
3. Traverse the string `s`:
   - If the current index `i == spaces[j]`, add a space `" "` and move `j++`.
   - Append `s[i]` to the result.
4. Join and return the final string.

**Time Complexity:** `O(n + m)` (where `n = len(s)`, `m = len(spaces)`)  
**Space Complexity:** `O(n + m)` (for the result string)

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution {
public:
    string addSpaces(string s, vector<int>& spaces) {
        string result;
        int j = 0;
        for (int i = 0; i < s.size(); i++) {
            if (j < spaces.size() && i == spaces[j]) {
                result.push_back(' ');
                j++;
            }
            result.push_back(s[i]);
        }
        return result;
    }
};

int main() {
    string s;
    int n;
    cout << "Enter string: ";
    cin >> s;
    cout << "Enter number of spaces: ";
    cin >> n;
    vector<int> spaces(n);
    cout << "Enter space indices: ";
    for (int i = 0; i < n; i++) cin >> spaces[i];

    Solution sol;
    cout << "Result: " << sol.addSpaces(s, spaces) << endl;
}
```

---
### **Java**
```Java

import java.util.*;

class Solution {
    public String addSpaces(String s, int[] spaces) {
        StringBuilder result = new StringBuilder();
        int j = 0;
        for (int i = 0; i < s.length(); i++) {
            if (j < spaces.length && i == spaces[j]) {
                result.append(' ');
                j++;
            }
            result.append(s.charAt(i));
        }
        return result.toString();
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter string: ");
        String s = sc.nextLine();
        System.out.print("Enter number of spaces: ");
        int n = sc.nextInt();
        int[] spaces = new int[n];
        System.out.println("Enter space indices:");
        for (int i = 0; i < n; i++) spaces[i] = sc.nextInt();

        Solution sol = new Solution();
        System.out.println("Result: " + sol.addSpaces(s, spaces));
    }
}
```
---

### **Python**
```Python
class Solution:
    def addSpaces(self, s, spaces):
        result = []
        j = 0
        for i in range(len(s)):
            if j < len(spaces) and i == spaces[j]:
                result.append(" ")
                j += 1
            result.append(s[i])
        return "".join(result)

if __name__ == "__main__":
    s = input("Enter string: ")
    n = int(input("Enter number of spaces: "))
    spaces = list(map(int, input("Enter space indices: ").split()))
    sol = Solution()
    print("Result:", sol.addSpaces(s, spaces))

```

---
### **JavaScript**
```JavaScript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    addSpaces(s, spaces) {
        let result = [];
        let j = 0;
        for (let i = 0; i < s.length; i++) {
            if (j < spaces.length && i === spaces[j]) {
                result.push(" ");
                j++;
            }
            result.push(s[i]);
        }
        return result.join("");
    }
}

readline.question("Enter string: ", (s) => {
    readline.question("Enter number of spaces: ", (nStr) => {
        const n = parseInt(nStr);
        readline.question("Enter space indices (space-separated): ", (arrStr) => {
            const spaces = arrStr.trim().split(" ").map(Number);
            const sol = new Solution();
            console.log("Result:", sol.addSpaces(s, spaces));
            readline.close();
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




