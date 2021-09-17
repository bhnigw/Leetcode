# \[Leetcode\]104. Maximum Depth of Binary Tree

原题地址：[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/) 关键词：DFS，BFS

题意：求树的高度/最大深度。

例：

![](../../.gitbook/assets/tmp-tree.jpg)

Input: `root = [3, 9, 20, null, null, 15, 7]`  
Output: 3



### 方法1：DFS / Recursion

* **终止条件:** 当前节点为空
* **返回值：**
  * 节点为空时，所以返回 0
  * 节点不为空时, 返回左右子树高度的最大值 + 1

```text
class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int maxLeft = maxDepth(root.left);
        int maxRight = maxDepth(root.right);
        
        return Math.max(maxLeft, maxRight) + 1;
    }
}
```

Time: `O(N)`；每个node走了一遍，所以时间是node的个数。

Space: `O(N)`；空间是DFS的stack个数，**也就是DFS的深度，也就是树的高度。**如果树的形状规则是balanced的，那平均时间是`O(logN)`；在worst case的情况下，树是一条向下的直线，深度为N，那么时间就是`O(N)`；



### 方法2：BFS

相当于level order traversal，每poll出一层深度加一；







