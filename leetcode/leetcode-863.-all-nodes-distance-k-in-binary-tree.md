---
description: BFS，DFS，Tree
---

# \[Leetcode\]★863. All Nodes Distance K in Binary Tree

原题地址：[https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/) 关键词：BFS，DFS，Tree，Queue，HashSet，HashMap

题意：给一个二叉树`root`， 和一个目标结点`target`，和一个整数值`K`。返回到`target`距离为`K`的所有结点。 答案可以任何顺序。

例如：  
求到节点5距离为2的所有节点

![](../.gitbook/assets/sketch0.png)

Input: `root = [3,5,1,6,2,0,8,null,null,7,4]`, `target = 5`, `k = 2`  
Output: `[7,4,1]`  
Explanation: The nodes that are a distance 2 from the target node \(with value 5\) have values 7, 4, and 1.



### 算法：BFS



```text
class Solution {
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        List<Integer> res = new ArrayList<>();
        HashMap<TreeNode, TreeNode> map = new HashMap<>();
        Set<TreeNode> visited = new HashSet<>();
        int level = 0;
        
        // DFS to record parent
        dfsToFindParent(root, map);
        
        // BFS
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(target);
        
        while (!queue.isEmpty()) {
            if (level == k) {              // 达到了目标层数k
                for (TreeNode node : queue) { 
                    res.add(node.val);    // 记录queue中所有node并返回
                }
                
                return res;
            }
            
            int size = queue.size();
            
            for (int i = 0; i < size; i++) { // 独立地poll光这一level
                TreeNode cur = queue.poll();
                visited.add(cur);
                if (cur.left != null && visited.add(cur.left)) {
                    queue.offer(cur.left); 
                }
                if (cur.right != null && visited.add(cur.right)) {
                    queue.offer(cur.right);
                }  
                if (map.get(cur) != null && visited.add(map.get(cur))) {
                    queue.offer(map.get(cur));
                }
            }
            
            level++;
        }
        
        return res;
    }
    
    private void dfsToFindParent(TreeNode root, HashMap<TreeNode, TreeNode> map) {
        if (root.left != null) {
            map.put(root.left, root);
            dfsToFindParent(root.left, map);
        }
        
        if (root.right != null) {
            map.put(root.right, root);
            dfsToFindParent(root.right, map);
        }
    }
}
```













