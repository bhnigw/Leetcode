---
description: Recursion
---

# \[Leetcode\]100. Same Tree

原题地址：[https://leetcode.com/problems/same-tree/](https://leetcode.com/problems/same-tree/) 关键词：DFS，Recursion

题意：判断两棵树是否完全相同。



### 算法：Recursion

如果两个树都为空，则两个树相同。如果两个树中有且只有一个为空，则两个树一定不相同。

如果两个树都不为空，那么首先判断它们的根节点的值是否相同，若不相同则两个二叉树一定不同，若相同，再分别判断两个树的左子树是否相同，以及右子树是否相同。这是一个Recursion过程，因此可以使用DFS，递归地判断两个二叉树是否相同。



（[一个小知识点](https://bhnigw.gitbook.io/-1/shu-ju-jie-gou-map#ru-guo-ba-treenode-jia-ru-hashmap)）

```text
class Solution {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;
        if (p == null || q == null) return false;
        
        if (p.val != q.val) return false;
        
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}

//Time: O(n); Space:O(logn)
```

Time: `O(M * N)`；  
解释：M和N分别是`root`和`subRoot`的节点总数，对于每一个`root`上的点，都需要做一次DFS来和`subRoot`匹配，匹配一次的时间代价是`O(N)`，那么总的时间代价就是`O(M * N)`

Space: `O(min(H1, H2))`；  
解释：H1和H2分别是两棵树度；为什么不直接是H1，因为input给出的`subRoot`深度有可能会比root大。



### 本题要记住的重点：

怎样避免nullPointerException❓



相关题目：

{% page-ref page="./" %}



