---
description: HashMap，BFS，graph
---

# \[Leetcode\]133. Clone Graph

原题地址：[https://leetcode.com/problems/clone-graph/](https://leetcode.com/problems/clone-graph/) 关键词：HashMap，BFS，graph

题意：Deep copy一个图。   
给一个undirected graph，每一个Node包含一个整数val，和一个List&lt;Node&gt;Neighbors作为它的adjacency list。不能返回它的reference，要返回它的deep copy。

例：

![](../.gitbook/assets/133_clone_graph_question.png)

Node的构造方法：

```text
class Node {
		public int val;
		public List<Node> neighbors;

		public Node() {
			this.val = 0;
			this.neighbors = new ArrayList<Node>();
		}

		public Node(int val) {
			this.val = val;
			this.neighbors = new ArrayList<Node>();
		}

		public Node(int val, ArrayList<Node> neighbors) {
			this.val = val;
			this.neighbors = neighbors;
		}
	}
```



算法：







完整代码：

```text
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        
        Map<Node, Node> visited = new HashMap<>();
        Node res = new Node(node.val, new ArrayList<>());
        visited.put(node, res);
        
        Queue<Node> queue = new LinkedList<>();
        queue.offer(node);
        
        while (!queue.isEmpty()) {
            Node curNode = queue.poll();
            
            for (Node eachNode : curNode.neighbors) {             
                if (!visited.containsKey(eachNode)) { //为什么不是containsValue
                    queue.offer(eachNode);
                    Node newNode = new Node(eachNode.val, new ArrayList<>());
                    visited.put(eachNode, newNode);
                }
                visited.get(curNode).neighbors.add(visited.get(eachNode)); 
                                                    //前面get的和后面的不一样
            } 
            
        }
        
        return res;
    }
}
```







