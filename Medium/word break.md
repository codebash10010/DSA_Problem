# Word Break - (LeetCode :- 139)

## 🏢 Companies Asked :- Amazon, Microsoft, Facebook, Google

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/word-break/)

---

## 🧩 Problem Statement

Given a string `s` and a dictionary of strings `wordDict`, return **true** if `s` can be segmented into a space-separated sequence of one or more dictionary words.

* All dictionary words can be reused any number of times.

---

## 💡 Intuition

* This is a **dynamic programming** problem.
* We can check all prefixes of `s` and see if they exist in the dictionary.

---

## ⚙️ Approach

1. Create a `dp` array of size `len(s)+1`, `dp[i] = true` if `s[0..i-1]` can be segmented.
2. Initialize `dp[0] = true`.
3. For each `i` from `1` to `len(s)`:

   * For each `j` from `0` to `i`:

     * If `dp[j]` is true and `s[j..i-1]` exists in `wordDict`, set `dp[i] = true`.
4. Return `dp[len(s)]`.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

bool wordBreak(string s, vector<string>& wordDict) {
    unordered_set<string> dict(wordDict.begin(), wordDict.end());
    vector<bool> dp(s.size() + 1, false);
    dp[0] = true;
    
    for(int i = 1; i <= s.size(); i++){
        for(int j = 0; j < i; j++){
            if(dp[j] && dict.count(s.substr(j,i-j))){
                dp[i] = true;
                break;
            }
        }
    }
    return dp[s.size()];
}

int main(){
    string s;
    int n;
    cin >> s >> n;
    vector<string> wordDict(n);
    for(int i=0;i<n;i++) cin >> wordDict[i];
    cout << (wordBreak(s, wordDict) ? "true" : "false") << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main {
    public static boolean wordBreak(String s, List<String> wordDict){
        Set<String> dict = new HashSet<>(wordDict);
        boolean[] dp = new boolean[s.length()+1];
        dp[0] = true;
        
        for(int i=1;i<=s.length();i++){
            for(int j=0;j<i;j++){
                if(dp[j] && dict.contains(s.substring(j,i))){
                    dp[i]=true;
                    break;
                }
            }
        }
        return dp[s.length()];
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String s = sc.next();
        int n = sc.nextInt();
        List<String> wordDict = new ArrayList<>();
        for(int i=0;i<n;i++) wordDict.add(sc.next());
        System.out.println(wordBreak(s, wordDict));
        sc.close();
    }
}
```

### 🐍 Python

```python
def wordBreak(s, wordDict):
    word_set = set(wordDict)
    dp = [False]*(len(s)+1)
    dp[0] = True
    
    for i in range(1,len(s)+1):
        for j in range(i):
            if dp[j] and s[j:i] in word_set:
                dp[i] = True
                break
    return dp[len(s)]

if __name__=="__main__":
    s = input().strip()
    n = int(input())
    wordDict = [input().strip() for _ in range(n)]
    print(wordBreak(s, wordDict))
```

### ⚡ JavaScript

```javascript
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
});

function wordBreak(s, wordDict){
    const wordSet = new Set(wordDict);
    const dp = Array(s.length+1).fill(false);
    dp[0] = true;

    for(let i=1;i<=s.length;i++){
        for(let j=0;j<i;j++){
            if(dp[j] && wordSet.has(s.slice(j,i))){
                dp[i] = true;
                break;
            }
        }
    }
    return dp[s.length];
}

let lines=[];
readline.on('line', line=>lines.push(line));
readline.on('close', ()=>{
    const s = lines[0].trim();
    const n = parseInt(lines[1]);
    const wordDict = lines.slice(2,2+n);
    console.log(wordBreak(s, wordDict));
});
```

---

## ⏱ Complexity

* **Time:** O(n³) (substring + DP)
* **Space:** O(n)

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
