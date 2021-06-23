---
description: Topological，Directed graph，HashMap，BFS
---

# \[Leetcode\]210. Course Schedule II

原题地址：[https://leetcode.com/problems/course-schedule-ii/](https://leetcode.com/problems/course-schedule-ii/)

与[207题](https://bhnigw.gitbook.io/leetcode/leetcode-207.-course-schedule)完全一样的思路，只是途中加入了一个数组记录Topological Sort的排序：

```text
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        int[] res = new int[numCourses];  
        int index = 0;
        
        //build the graph
        int[] inDegree = new int[numCourses];
        HashMap<Integer, List<Integer>> graph = new HashMap<>();
        for (int i = 0; i < prerequisites.length; i++) {
            if (graph.get(prerequisites[i][1]) == null) {
                inDegree[prerequisites[i][0]]++;
                graph.put(prerequisites[i][1], new ArrayList<Integer>());
                graph.get(prerequisites[i][1]).add(prerequisites[i][0]);
            } else {
                inDegree[prerequisites[i][0]]++;
                graph.get(prerequisites[i][1]).add(prerequisites[i][0]);
            }
        }
        
        //build queue
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
                res[index] = i;
                index++;
            }
        }
        
        //bfs
        while (!queue.isEmpty()) {
            int course = queue.poll();
            List<Integer> toTake = graph.get(course);
            
            for (int i = 0; toTake != null && i < toTake.size(); i++) {
                inDegree[toTake.get(i)]--;
                if (inDegree[toTake.get(i)] == 0) {
                    queue.offer(toTake.get(i));
                    res[index] = toTake.get(i);
                    index++;
                }
            }
        }
        
        // check inDegree
        for (int i = 0; i < numCourses; i++) {
            if (inDegree[i] != 0) {
                res = new int[0];
            }
        }
        
        return res;
    }
}
```

总结代码结构：  
1. Build graph;  
2. Build the queue;  
3. BFS  
4. Check inDegree

