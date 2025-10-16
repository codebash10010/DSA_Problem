# Longest Increasing Subsequence - (LeetCode :- 300)

## 🏢 Companies Asked :- Amazon, Google, Microsoft, Facebook

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/longest-increasing-subsequence/)

---

## 🧩 Problem Statement

Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

---

## 📌 Constraints

* `1 <= nums.length <= 2500`
* `-10^4 <= nums[i] <= 10^4`

---

## 💡 Intuition

* For each element, find the length of the **longest increasing subsequence ending at that element**.
* Use **Dynamic Programming**.

---

## ⚙️ Approach (DP)

1. Create an array `dp` of size `n`, initialize all with `1` (each element is a subsequence of length 1).
2. For each `i` from 0 to n-1:

   * For each `j` from 0 to i-1:

     * If `nums[i] > nums[j]`, update `dp[i] = max(dp[i], dp[j] + 1)`
3. Return `max(dp)`.

---

## 🧩 Code Implementations (with user input)

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

int lengthOfLIS(vector<int>& nums) {
    int n = nums.size();
    vector<int> dp(n, 1);
    for(int i=0;i<n;i++){
        for(int j=0;j<i;j++){
            if(nums[i]>nums[j]) dp[i]=max(dp[i], dp[j]+1);
        }
    }
    return *max_element(dp.begin(), dp.end());
}

int main(){
    int n;
    cin >> n;
    vector<int> nums(n);
    for(int i=0;i<n;i++) cin >> nums[i];
    cout << lengthOfLIS(nums) << endl;
}
```

### ☕ Java

```java
import java.util.*;

public class Main{
    public static int lengthOfLIS(int[] nums){
        int n=nums.length;
        int[] dp=new int[n];
        Arrays.fill(dp,1);
        for(int i=0;i<n;i++){
            for(int j=0;j<i;j++){
                if(nums[i]>nums[j]) dp[i]=Math.max(dp[i], dp[j]+1);
            }
        }
        int max=0;
        for(int val:dp) max=Math.max(max,val);
        return max;
    }
    
    public static void main(String[] args){
        Scanner sc=new Scanner(System.in);
        int n=sc.nextInt();
        int[] nums=new int[n];
        for(int i=0;i<n;i++) nums[i]=sc.nextInt();
        System.out.println(lengthOfLIS(nums));
        sc.close();
    }
}
```

### 🐍 Python

```python
def lengthOfLIS(nums):
    n=len(nums)
    dp=[1]*n
    for i in range(n):
        for j in range(i):
            if nums[i]>nums[j]:
                dp[i]=max(dp[i], dp[j]+1)
    return max(dp)

if __name__=="__main__":
    n=int(input())
    nums=list(map(int,input().split()))
    print(lengthOfLIS(nums))
```

### ⚡ JavaScript

```javascript
const readline=require('readline').createInterface({
    input:process.stdin,
    output:process.stdout
});

function lengthOfLIS(nums){
    const n=nums.length;
    const dp=Array(n).fill(1);
    for(let i=0;i<n;i++){
        for(let j=0;j<i;j++){
            if(nums[i]>nums[j]) dp[i]=Math.max(dp[i], dp[j]+1);
        }
    }
    return Math.max(...dp);
}

let lines=[];
readline.on('line', line=>lines.push(line));
readline.on('close', ()=>{
    const n=parseInt(lines[0]);
    const nums=lines[1].split(' ').map(Number);
    console.log(lengthOfLIS(nums));
});
```

---

## ⏱ Complexity

* **Time:** O(n²)
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
