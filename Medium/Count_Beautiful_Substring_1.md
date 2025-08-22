# Count Beautiful Substrings - (LeetCode :- 2947)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Adobe  
👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)
---

## 🔗 Problem Link
You can find the original problem here:  
👉 https://leetcode.com/problems/count-beautiful-substrings-i/

---

## 📝 Problem Statement

You are given a string `s` and a positive integer `k`.  

- Let **vowels** = number of vowels in the substring.  
- Let **consonants** = number of consonants in the substring.  

A string is **beautiful** if:

1. `vowels == consonants`  
2. `(vowels * consonants) % k == 0`  

Return the number of **non-empty beautiful substrings** in the given string `s`.  

A **substring** is a contiguous sequence of characters in a string.  

👉 Vowel letters in English: **a, e, i, o, u**  
👉 Consonant letters: Every other English lowercase letter  

---

## 📌 Constraints
- `1 <= s.length <= 1000`  
- `1 <= k <= 1000`  
- `s` consists of only **English lowercase letters**

---

## 📌 Examples

### **Example 1**

**Input:**  
s = "baeyh", k = 2

**Output:**  
2

**Explanation:**  
Beautiful substrings:  
- `"baeyh"` → vowels = {a, e}, consonants = {y, h} → 2 vowels, 2 consonants → ✔️  
- `"baey"` → vowels = {a, e}, consonants = {b, y} → 2 vowels, 2 consonants → ✔️  

---

### **Example 2**

**Input:**  
s = "abba", k = 1

**Output:**  
3


**Explanation:**  
Beautiful substrings:  
- `"ab"` → vowels = {a}, consonants = {b} → ✔️  
- `"ba"` → vowels = {a}, consonants = {b} → ✔️  
- `"abba"` → vowels = {a,a}, consonants = {b,b} → ✔️  

---

### **Example 3**

**Input:**  
s = "bcdf", k = 1

**Output:**  
0


**Explanation:**  
There are no substrings with equal vowels and consonants.  

---

## 💡 Intuition Behind the Approach

1. **Brute Force (Naive Thinking):**  
   - Generate all substrings → Count vowels & consonants → Check conditions.  
   - Time complexity → `O(n^3)` (too slow for `n=1000`).  

2. **Optimized Approach:**  
   - Use **prefix sums** to track vowel and consonant counts efficiently.  
   - For each substring `(i, j)`,  
     - Vowels = prefixVowels[j] - prefixVowels[i-1]  
     - Consonants = prefixCons[j] - prefixCons[i-1]  
   - Check: `vowels == consonants` and `(vowels * consonants) % k == 0`.  

👉 This reduces substring check to **O(n^2)**.  

---

## 📚 Algorithm Explanation

1. Precompute two prefix arrays:  
   - `prefixVowels[i]` = number of vowels up to index `i`.  
   - `prefixCons[i]` = number of consonants up to index `i`.  

2. Iterate over all possible substrings `(i, j)`:
   - Get vowel and consonant count from prefix arrays.  
   - Check conditions:  
     - `vowels == consonants`  
     - `(vowels * consonants) % k == 0`  

3. Maintain a counter and return the result.  

**Time Complexity:** `O(n^2)`  
**Space Complexity:** `O(n)`  

---

## 💻 Implementations

### **C++**
```cpp
#include <iostream>
#include <vector>
#include <string>
using namespace std;

class Solution {
    bool isVowel(char c) {
        return c=='a' || c=='e' || c=='i' || c=='o' || c=='u';
    }
public:
    int beautifulSubstrings(string s, int k) {
        int n = s.size(), count = 0;
        vector<int> vowelPrefix(n+1,0), consPrefix(n+1,0);

        for(int i=0; i<n; i++){
            vowelPrefix[i+1] = vowelPrefix[i] + (isVowel(s[i]) ? 1 : 0);
            consPrefix[i+1] = consPrefix[i] + (!isVowel(s[i]) ? 1 : 0);
        }

        for(int i=0; i<n; i++){
            for(int j=i; j<n; j++){
                int vowels = vowelPrefix[j+1] - vowelPrefix[i];
                int cons = consPrefix[j+1] - consPrefix[i];
                if(vowels == cons && (vowels * cons) % k == 0) {
                    count++;
                }
            }
        }
        return count;
    }
};

int main(){
    string s; int k;
    cout << "Enter string: ";
    cin >> s;
    cout << "Enter k: ";
    cin >> k;
    Solution sol;
    cout << "Beautiful substrings: " << sol.beautifulSubstrings(s, k) << endl;
}

```
---

### **Java**
```Java

import java.util.*;

class Solution {
    private boolean isVowel(char c) {
        return "aeiou".indexOf(c) != -1;
    }
    
    public int beautifulSubstrings(String s, int k) {
        int n = s.length(), count = 0;
        int[] vowelPrefix = new int[n+1], consPrefix = new int[n+1];

        for (int i = 0; i < n; i++) {
            vowelPrefix[i+1] = vowelPrefix[i] + (isVowel(s.charAt(i)) ? 1 : 0);
            consPrefix[i+1] = consPrefix[i] + (!isVowel(s.charAt(i)) ? 1 : 0);
        }

        for (int i = 0; i < n; i++) {
            for (int j = i; j < n; j++) {
                int vowels = vowelPrefix[j+1] - vowelPrefix[i];
                int cons = consPrefix[j+1] - consPrefix[i];
                if (vowels == cons && (vowels * cons) % k == 0) count++;
            }
        }
        return count;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter string: ");
        String s = sc.next();
        System.out.print("Enter k: ");
        int k = sc.nextInt();
        Solution sol = new Solution();
        System.out.println("Beautiful substrings: " + sol.beautifulSubstrings(s, k));
    }
}

```
---
### **Python**
```Python


class Solution:
    def beautifulSubstrings(self, s: str, k: int) -> int:
        def is_vowel(c): return c in "aeiou"
        n = len(s)
        vowel_prefix = [0] * (n+1)
        cons_prefix = [0] * (n+1)

        for i in range(n):
            vowel_prefix[i+1] = vowel_prefix[i] + (1 if is_vowel(s[i]) else 0)
            cons_prefix[i+1] = cons_prefix[i] + (0 if is_vowel(s[i]) else 1)

        count = 0
        for i in range(n):
            for j in range(i, n):
                vowels = vowel_prefix[j+1] - vowel_prefix[i]
                cons = cons_prefix[j+1] - cons_prefix[i]
                if vowels == cons and (vowels * cons) % k == 0:
                    count += 1
        return count

if __name__ == "__main__":
    s = input("Enter string: ")
    k = int(input("Enter k: "))
    sol = Solution()
    print("Beautiful substrings:", sol.beautifulSubstrings(s, k))


```
---

### **JavaScript**
```JavaScript

const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout,
});

class Solution {
    isVowel(c) {
        return "aeiou".includes(c);
    }
    beautifulSubstrings(s, k) {
        let n = s.length, count = 0;
        let vowelPrefix = Array(n+1).fill(0);
        let consPrefix = Array(n+1).fill(0);

        for (let i = 0; i < n; i++) {
            vowelPrefix[i+1] = vowelPrefix[i] + (this.isVowel(s[i]) ? 1 : 0);
            consPrefix[i+1] = consPrefix[i] + (!this.isVowel(s[i]) ? 1 : 0);
        }

        for (let i = 0; i < n; i++) {
            for (let j = i; j < n; j++) {
                let vowels = vowelPrefix[j+1] - vowelPrefix[i];
                let cons = consPrefix[j+1] - consPrefix[i];
                if (vowels === cons && (vowels * cons) % k === 0) {
                    count++;
                }
            }
        }
        return count;
    }
}

readline.question("Enter string: ", (s) => {
    readline.question("Enter k: ", (kStr) => {
        let k = parseInt(kStr);
        const sol = new Solution();
        console.log("Beautiful substrings:", sol.beautifulSubstrings(s, k));
        readline.close();
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
