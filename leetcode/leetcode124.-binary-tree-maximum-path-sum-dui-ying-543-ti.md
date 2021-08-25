---
description: Tree，DFS
---

# \[Leetcode\]★124. Binary Tree Maximum Path Sum \(对应543题\)

原题地址：[https://leetcode.com/problems/binary-tree-maximum-path-sum/](https://leetcode.com/problems/binary-tree-maximum-path-sum/) 关键词：Tree，DFS

题意：求最大路径和。  
给一个二叉树，每两个node之间都有一条唯一的路径。路径和就是路径中各节点值val的总和。路径不一定经过根节点。

例子：

![](../.gitbook/assets/exx2.jpg)

Input: `root = [-10,9,20,null,null,15,7]`   
Output: 42   
Explanation: 最优路径是`15 -> 20 -> 7`，路径和为`15 + 20 + 7 = 42`



### 算法：DFS

★**核心思想:** 对于每一个node，**`穿过它的最大路径和` = `穿过左child的最大路径和` + `穿过右child的最大路径和`**



初始化一个长度为1的`res[]`数组来记录结果；Recursion的过程：从最底层leaf向上，对当前的node，拿到它左child的最大路径和，和它右child的最大路径和，然后加上当前node的val，即为穿过该node的最大路径和sum。

然后，把这个sum与global变量`res[]`里的值做一个对比，更新最大的sum。

接下来，向上recursion，向它的parent node返回一个最大的和。如果parent node一旦选择走这个node，那就要加上这个最大的和。事实上，parent node会**在自己的左右两个child中选择一个对sum贡献更大的来走。**

**❗️**这就是本题的难点，要弄清楚Recursion时我们要返回的是什么！！  
我们的目标：判断parent node到底要走左右child哪一条路！  
怎样判断：选路径和最大的那条路走！  
所以我们返回的是：该node能给parent贡献的最大路径和！  
**`该node能给parent贡献的最大路径和` = `Max(该node左child的最大和, 该node右child的最大和) + parent.val`**

⚠️  注意：如果此时求出的这个`"能给parent贡献的最大路径和"`的值为负数，说明此条经过该node的路径，对求最大路径和一点帮助都没有！应该舍弃掉它。所以如果遇到负数就把`"能给parent贡献的最大路径和"`的值设为0；（见代码第18行）

```text
class Solution {
    public int maxPathSum(TreeNode root) {
        int[] res = new int[]{Integer.MIN_VALUE}; // 可能会和负数比较，所以设为最小整数
        
        dfs(root, res);
        
        return res[0];
    }
    
    private int dfs(TreeNode root, int[] res) {
        if (root == null) return 0;
        
        int leftMaxSum = dfs(root.left, res);
        int rightMaxSum = dfs(root.right, res);
        
        res[0] = Math.max(res[0], leftMaxSum + rightMaxSum + root.val);
        
        return Math.max(Math.max(leftMaxSum, rightMaxSum) + root.val, 0); 
                                                                  //注意为什么是0
    }
}
```

Time: `O(N)`；每个node走了一遍，所以时间是node的个数。

Space: `O(N)`；空间是DFS的stack个数，**也就是DFS的深度，也就是树的高度。**如果树的形状规则，那平均时间是`O(logN)`；在worst case的情况下，树是一条向下的直线，深度为N，那么时间就是`O(N)`；



### 要记住的重点：

1. 用`res[]`来记录结果
2. `res[0]`来的初始值是Integer.MIN\_VALUE
3. DFS时返回的是什么？是返回该node能给parent贡献的最大sum

  
同类题：

{% page-ref page="leetcode-543.-diameter-of-binary-tree.md" %}







