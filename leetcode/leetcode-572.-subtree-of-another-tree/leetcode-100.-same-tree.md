---
description: Recursion
---

# \[Leetcode]100. Same Tree

原题地址：[https://leetcode.com/problems/same-tree/](https://leetcode.com/problems/same-tree/) 关键词：DFS，Recursion

题意：判断两棵树是否完全相同。



### 算法：Recursion

如果两个树都为空，则两个树相同。如果两个树中有且只有一个为空，则两个树一定不相同。

如果两个树都不为空，那么首先判断它们的根节点的值是否相同，若不相同则两个二叉树一定不同，若相同，再分别判断两个树的左子树是否相同，以及右子树是否相同。这是一个Recursion过程，因此可以使用DFS，递归地判断两个二叉树是否相同。



（[一个小知识点](https://bhnigw.gitbook.io/1/shu-ju-jie-gou-map#ru-guo-ba-treenode-jia-ru-hashmap)）

```
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

Time: `O(min(M, N))`；\
解释：M和N分别是两棵树的节点总数，只有当两个二叉树中的对应节点都不为空时才会访问到该节点，因此被访问到的节点数不会超过较小的二叉树的节点数。

Space: `O(min(H1, H2))`；\
解释：H1和H2分别是两棵树的高度；空间复杂度取决于递归调用的层数，递归调用的层数不会超过较小的二叉树的最大高度。



### 本题要记住的重点：

1. 怎样避免nullPointerException❓
2. 复杂度计算；





相关题目：

{% content-ref url="./" %}
[.](./)
{% endcontent-ref %}

