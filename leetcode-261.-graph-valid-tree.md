---
description: 'Union find, Undirected graph'
---

# \[Leetcode\]261. Graph Valid Tree

原题地址：[https://leetcode.com/problems/graph-valid-tree/](https://leetcode.com/problems/graph-valid-tree/)关键词：Union find, Undirected graph

题意：判断树。给一个数字n，表示有0到n-1个节点；给一个`edges[][]`，根据它做出一个无向图；**判断作出的图是不是一个tree**，是就true；

Example 1：

![](.gitbook/assets/tree1-graph.jpg)

`Input: n = 5, edges = [[0,1],[0,2],[0,3],[1,4]]   
Output: true`

Example 2：

![](.gitbook/assets/tree2-graph-copy.jpg)

`Input: n = 5, edges = [[1,2],[2,3],[1,3],[1,4]]   
Output: false`

### 方法一：Graph DFS with adjacency list



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

