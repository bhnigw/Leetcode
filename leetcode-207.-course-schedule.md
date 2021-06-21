---
description: Topological，Directed graph，HashMap，BFS
---

# \[Leetcode\]207. Course Schedule

原题地址：[https://leetcode.com/problems/course-schedule/](https://leetcode.com/problems/course-schedule/) 关键词：Topological, Directed graph，BFS

题意：某学期必须选修 n 门课程，记为 0 到 n - 1 ;（比如必须选5门课，那么课程号就为0,1,2,3,4）  
在选修某些课程之前需要一些先修课程。 先修课程按数组`prerequisites[]`给出，其中`prerequisites[i] = [ai, bi]` ，表示如果要学习课程 ai 则必须先学习课程 bi 。  
例如，先修课程对 \[0, 1\] 表示：想要学习课程 0 ，你需要先完成课程 1 。   
请你判断是否可能完成所有课程的学习？如果可以，返回 true ；否则返回 false 。

Example 1:  
Input: `numCourses = 2`, `prerequisites = [[1,0]]`;   
Output: `true` 

Example 2:  
Input: `numCourses = 2`, `prerequisites = [[1,0],[0,1]]`;  
 Output: `false`



### 方法一：构建有向图，检查环

假设需要选5门课，先修课的要求为：`prerequisites = [[1, 0], [0, 2], [3, 4], [4, 0], [2, 1]]`;那么可以用课程号指向先修课，就构成了一个有向图：

![](.gitbook/assets/207_graph.png)

那么这道题就演变成了[Detect whether a directed graph has a loop or cycle. ](https://app.gitbook.com/@bhnigw/s/leetcode/~/drafts/-McNcLDMFP7Hl_JYsmTd/ji-chu-bi-hui/detect-cycle-in-a-directed-graph)（点击查看详细图解）

#### 算法：

第一步：  
我们可以用一个HashMap和ArrayList来记录这个有向图：`HashMap<Integer, ArrayList<Integer>()> map = new HashMap<>();`

其中，map的key记录当前节点；  
            map的value记录**由当前点出发，指向的别的点的值；**

那么上面的有向图就可以用HashMap表示为：  
`{0 = [2],   
1 = [0],   
2 = [1],   
3 = [4],   
4 = [0]}`



第二步：  
我们初始化一个boolean的数组，长度为课程总数numCourses：`boolean[] visited = new boolean[numCourses];`（boolean的初始值默认都是false）

这个`visited[]`boolean数组用来记录我们遍历已经访问过的node；



第三步：  
使用backtracking

1. 首先构建这个graph存到map；
2. 然后遍历map；
3. 把走过的节点都在`visited[]`里标记true，backtrack回去时变回false；
4. 在遍历时如果遇到true，说明已经访问过，说明有loop/cycle；

在backtrack时，用下面两个if放在前面判断：  
`if (visited[cur] == true) return true; //若已访问过，说明有loop   
if (map.get(cur) == null) return false; //为null说明当前点没有子节点，为终点`

backtrack完成时，要把visited变回false：  
`visited[cur] = false;`

```text
class Solution {
  public boolean canFinish(int numCourses, int[][] prerequisites) {

    HashMap<Integer, List<Integer>> map = new HashMap<>();

    // build the graph
    for (int i = 0; i < prerequisites.length; i++) {
        if (map.get(prerequisites[i][0]) == null) {
            map.put(prerequisites[i][0], new ArrayList<Integer>());
            map.get(prerequisites[i][0]).add(prerequisites[i][1]);
        } else {
            map.get(prerequisites[i][0]).add(prerequisites[i][1]);
        }
    }

    boolean[] visited = new boolean[numCourses];

    for (int i = 0; i < numCourses; i++) {
      if (isCycle(i, map, visited)) {
        return false;
      }
    }

    return true;
  }


  private boolean isCycle(int cur, HashMap<Integer, List<Integer>> map, boolean[] visited) {
      if (visited[cur] == true) return true;
      if (map.get(cur) == null) return false;
      
      List<Integer> temp = new ArrayList<>(map.get(cur));    
      visited[cur] = true;
      
      for (int j = 0; j < temp.size(); j++) {
          if (isCycle(temp.get(j), map, visited)) {
              return true;
          }
      }
      
      visited[cur] = false; //注意要变回false
      
      return false;
  }
}
```

Time:??  
Space:?



### 方法二（重要）：拓扑排序 Topological Sort

有向图中的一些概念：  
入度\(`In-Degree`\)：；  
出度\(`Out-Degree`\)：；











