---
description: undirected graph，bidirectional
---

# 无向图中检查环 Detect cycle in a undirected graph

### 怎样检测一个无向图undirected graph里是否有环？？

假设一个图有n=5个节点，给出一个`edges = [[0,1],[1,2],[2,3],[1,3],[1,4]]`，做出下图。肉眼可以观察到有一个`1 -> 2 -> 3 -> 1`组成的cycle，但是怎样用程序来鉴别呢？

![](../.gitbook/assets/tree2-graph.jpg)

#### 第一个问题：怎样记录和表示一个无向图？

要注意的是，无向图中所有的边都是双向的\(**All edges are bidirectional！**\)，所以我们需要一个数据结构能记录每个点，以及和每个点所有相连接的点。

我们可以用一个**Adjacency List**来记录（也就是一个二维的ArrayList）：  
`List<List<Integer>> adjList = new ArrayList<>();`

其中，adjList的index为图的n个节点；  
            adjList.get\(index\)的记录**与当前节点所有；**

那么上面的无向图就可以表示为：  
`0 : [1],   
1 : [0, 2, 3, 4],   
2 : [1, 3],   
3 : [1, 2],   
4 : [1]`

