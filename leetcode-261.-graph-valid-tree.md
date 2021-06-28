---
description: Union find，Undirected graph，DFS
---

# \[Leetcode\]261. Graph Valid Tree

原题地址：[https://leetcode.com/problems/graph-valid-tree/](https://leetcode.com/problems/graph-valid-tree/)关键词：Union find, Undirected graph, DFS

题意：判断树。给一个数字n，表示有0到n-1个节点；给一个`edges[][]`，根据它做出一个无向图undirected graph；**判断作出的图是不是一个tree**，是就true；

Example 1：

![](.gitbook/assets/tree1-graph.jpg)

`Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]   
Output: true`

Example 2：

![](.gitbook/assets/tree2-graph-copy.jpg)

`Input: n = 5, edges = [[1,2],[2,3],[1,3],[1,4]]   
Output: false`



### 注意：

**如果一个图是tree，那么它必须满足以下条件/具有以下特点：**  
1. 任何两个节点之间都有一条连接的路径；也就是说，所有点都必须fully connected，不能有落单的；  
2. 图中不能有环cycle/loop；  
★3. **如果一个tree有n个节点，那么它必然有n - 1条edges**；若少于n - 1则必然有点没有连接上，若多于n - 1则必然有环cycle/loop



### 方法一：Graph DFS with adjacency list

基本算法步骤：  
1. 检查图中是否有环；  
2. 检查所有节点是否都连接上；

对于第1点，检查有环，参考[检测无向图中是否存在环](https://bhnigw.gitbook.io/leetcode/ji-chu-bi-hui/wu-xiang-tu-zhong-jian-cha-huan-detect-cycle-inaundirected-graph)；  
**算法步骤：**

1. 根据tree特点，如果edges总数不等于n - 1，直接false；
2. 构建adjacency list；
3. 新建boolean数组`visited[]`记录已经访问过的节点；
4. DFS

★最后记得第2点，检查所有节点是否都连接上；

```text
class Solution {
    public boolean validTree(int n, int[][] edges) {
        if (edges.length != n - 1) return false;
        
        // initialize adjacency list
        List<List<Integer>> adjList = new ArrayList<>();
        for (int i = 0; i < n; i++) { //注意这里是n
            adjList.add(i, new ArrayList<Integer>());
        }

        // Add edges
        for (int i = 0; i < edges.length; i++) {
            adjList.get(edges[i][0]).add(edges[i][1]);
            adjList.get(edges[i][1]).add(edges[i][0]);
        }
        
        
        // dfs
        boolean[] visited = new boolean[n];
        if (hasCycle(adjList, visited, 0, -1)) { //起始点0没有parentNode，所以是-1
            return false;
        }
        
        // make sure all vertices are connected
        for (boolean i : visited) {
            if (i == false) {
                return false; //居然还有一个节点没有被访问过，说明不是图
            }
        }
        
        return true;
    }
    
    private boolean hasCycle(List<List<Integer>> adjList, boolean[] visited, int curNode, int parentNode) {
        if (visited[curNode] == true) return true; //如果true说明已访问过，说明出现环
        
        visited[curNode] = true;
        List<Integer> childNode = adjList.get(curNode);
        
        for (int i : childNode) {
            if (parentNode != i && hasCycle(adjList, visited, i, curNode)) {
                return true;
            }
        }
        
        return false;
    }
}
```



方法二：
