# Is Graph Bipartite - (LeetCode :- 785)

## 🏢 Companies Asked :- Amazon ✯, Google ✯, Microsoft ✯, Facebook ✯

👉 [Watch on YouTube](https://youtube.com/@codebash10010?si=_iT9ZHNks9ZaN4d5)
👉 [Watch on Instagram](https://www.instagram.com/codebash.official/)

**Difficulty:** 🟠 Medium

[🔗 Problem Link](https://leetcode.com/problems/is-graph-bipartite/)

---

## 🧩 Problem Statement

Given an undirected graph `graph` where `graph[i]` is a list of nodes connected to node `i`, return **true** if the graph is bipartite.

A graph is bipartite if the nodes can be colored with 2 colors such that no two adjacent nodes have the same color.

---

## 💡 Intuition

* Bipartite graph check = can we color nodes with 2 colors?
* Use **BFS** or **DFS** to assign colors.
* If any neighbor has the same color → Not bipartite.

---

## ⚙️ Approach

1. Initialize `color` array: -1 (unvisited).
2. For each unvisited node:

   * Use BFS/DFS to color nodes alternately (0 or 1).
   * If a neighbor has the same color → return false.
3. If all nodes colored without conflict → return true.

---

## 🧩 Code Implementations

### 🧱 C++

```cpp
#include <bits/stdc++.h>
using namespace std;

bool dfs(int node, int c, vector<int> &color, vector<vector<int>> &graph){
    color[node] = c;
    for(int nbr : graph[node]){
        if(color[nbr]==-1){
            if(!dfs(nbr, 1-c, color, graph)) return false;
        } else if(color[nbr]==c) return false;
    }
    return true;
}

bool isBipartite(vector<vector<int>> &graph){
    int n = graph.size();
    vector<int> color(n, -1);
    for(int i=0;i<n;i++){
        if(color[i]==-1 && !dfs(i,0,color,graph)) return false;
    }
    return true;
}

int main(){
    int n;
    cin >> n;
    vector<vector<int>> graph(n);
    for(int i=0;i<n;i++){
        int m; cin >> m;
        graph[i].resize(m);
        for(int j=0;j<m;j++) cin >> graph[i][j];
    }
    cout << (isBipartite(graph) ? "true" : "false") << "\n";
}
```

---

### ☕ Java

```java
import java.util.*;

public class Main{
    static boolean dfs(int node, int c, int[] color, List<List<Integer>> graph){
        color[node] = c;
        for(int nbr : graph.get(node)){
            if(color[nbr]==-1){
                if(!dfs(nbr,1-c,color,graph)) return false;
            } else if(color[nbr]==c) return false;
        }
        return true;
    }

    static boolean isBipartite(List<List<Integer>> graph){
        int n = graph.size();
        int[] color = new int[n];
        Arrays.fill(color,-1);
        for(int i=0;i<n;i++){
            if(color[i]==-1 && !dfs(i,0,color,graph)) return false;
        }
        return true;
    }

    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();
        for(int i=0;i<n;i++){
            int m = sc.nextInt();
            List<Integer> list = new ArrayList<>();
            for(int j=0;j<m;j++) list.add(sc.nextInt());
            graph.add(list);
        }
        System.out.println(isBipartite(graph));
        sc.close();
    }
}
```

---

### 🐍 Python

```python
def isBipartite(graph):
    n = len(graph)
    color = [-1]*n
    def dfs(node, c):
        color[node] = c
        for nbr in graph[node]:
            if color[nbr]==-1:
                if not dfs(nbr,1-c):
                    return False
            elif color[nbr]==c:
                return False
        return True

    for i in range(n):
        if color[i]==-1 and not dfs(i,0):
            return False
    return True

if __name__=="__main__":
    n = int(input())
    graph = []
    for _ in range(n):
        lst = list(map(int,input().split()))
        graph.append(lst)
    print(isBipartite(graph))
```

---

### ⚡ JavaScript

```javascript
const readline = require("readline").createInterface({
    input: process.stdin,
    output: process.stdout
});

function isBipartite(graph){
    const n = graph.length;
    const color = Array(n).fill(-1);

    function dfs(node, c){
        color[node] = c;
        for(let nbr of graph[node]){
            if(color[nbr]===-1){
                if(!dfs(nbr,1-c)) return false;
            } else if(color[nbr]===c){
                return false;
            }
        }
        return true;
    }

    for(let i=0;i<n;i++){
        if(color[i]===-1 && !dfs(i,0)) return false;
    }
    return true;
}

readline.question("Enter number of nodes: ", n => {
    n = parseInt(n);
    let count = 0;
    let graph = Array(n).fill(0).map(()=>[]);
    function readGraphLine(){
        if(count>=n){
            console.log(isBipartite(graph));
            readline.close();
            return;
        }
        readline.question("", line=>{
            graph[count] = line.trim().split(" ").map(Number);
            count++;
            readGraphLine();
        });
    }
    readGraphLine();
});
```

---

### Sample Input

```
4
1 3
0 2
1 3
0 2
```

### Output

```
true
```

---

### Complexity

* **Time:** O(V + E)
* **Space:** O(V)

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


