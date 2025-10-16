# Candy - (LeetCode :- 135)

## 🏢 Companies Asked :- Amazon, Google, Facebook, Microsoft

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/candy/description/)

---

## 🧩 Problem Statement

There are `n` children standing in a line. Each child is assigned a rating value given in the integer array `ratings`.

* You are giving candies to these children subject to the following requirements:

  1. Each child must have **at least one candy**.
  2. Children with a higher rating get **more candies** than their neighbors.

Return **the minimum number of candies** you need to have to distribute the candies to the children.

---

## 💡 Intuition

* Assign **1 candy** to each child initially.
* Make **two passes**: left→right, then right→left to ensure the higher-rated child gets more candies than neighbors.

---

## ⚙️ Approach

1. Initialize `candies[i] = 1` for all children.
2. **Left to right:** if `ratings[i] > ratings[i-1]`, then `candies[i] = candies[i-1] + 1`.
3. **Right to left:** if `ratings[i] > ratings[i+1]`, then `candies[i] = max(candies[i], candies[i+1]+1)`.
4. Sum all `candies` to get the answer.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int candy(vector<int>& ratings) {
    int n = ratings.size();
    vector<int> candies(n,1);
    for(int i=1;i<n;i++){
        if(ratings[i]>ratings[i-1]) candies[i]=candies[i-1]+1;
    }
    for(int i=n-2;i>=0;i--){
        if(ratings[i]>ratings[i+1]) candies[i]=max(candies[i],candies[i+1]+1);
    }
    return accumulate(candies.begin(),candies.end(),0);
}

int main(){
    int n;
    cin >> n;
    vector<int> ratings(n);
    for(int i=0;i<n;i++) cin >> ratings[i];
    cout << candy(ratings) << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main{
    public static int candy(int[] ratings){
        int n = ratings.length;
        int[] candies = new int[n];
        Arrays.fill(candies,1);
        
        for(int i=1;i<n;i++){
            if(ratings[i]>ratings[i-1]) candies[i]=candies[i-1]+1;
        }
        for(int i=n-2;i>=0;i--){
            if(ratings[i]>ratings[i+1]) candies[i]=Math.max(candies[i],candies[i+1]+1);
        }
        
        int sum = 0;
        for(int c: candies) sum+=c;
        return sum;
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] ratings = new int[n];
        for(int i=0;i<n;i++) ratings[i]=sc.nextInt();
        System.out.println(candy(ratings));
        sc.close();
    }
}
```

### 🐍 Python

```python
def candy(ratings):
    n = len(ratings)
    candies = [1]*n
    for i in range(1,n):
        if ratings[i]>ratings[i-1]:
            candies[i]=candies[i-1]+1
    for i in range(n-2,-1,-1):
        if ratings[i]>ratings[i+1]:
            candies[i]=max(candies[i],candies[i+1]+1)
    return sum(candies)

if __name__=="__main__":
    n=int(input())
    ratings=list(map(int,input().split()))
    print(candy(ratings))
```

### ⚡ JavaScript

```javascript
const readline = require('readline').createInterface({
  input: process.stdin,
  output: process.stdout
});

function candy(ratings){
    const n = ratings.length;
    const candies = Array(n).fill(1);

    for(let i=1;i<n;i++){
        if(ratings[i]>ratings[i-1]) candies[i]=candies[i-1]+1;
    }
    for(let i=n-2;i>=0;i--){
        if(ratings[i]>ratings[i+1]) candies[i]=Math.max(candies[i],candies[i+1]+1);
    }
    return candies.reduce((a,b)=>a+b,0);
}

let lines=[];
readline.on('line', line=>lines.push(line));
readline.on('close', ()=>{
    const n=parseInt(lines[0]);
    const ratings = lines[1].split(" ").map(Number);
    console.log(candy(ratings));
});
```

---

## ⏱ Complexity

* **Time:** O(n)
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
