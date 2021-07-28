---
description: Binary Search Tree
---

# 查找 Search

原题地址：[https://leetcode.com/problems/search-in-a-binary-search-tree/](https://leetcode.com/problems/search-in-a-binary-search-tree/) 关键词：Binary Search Tree

题意：给定Binary Search Tree的根节点`root`和一个值`val`。 需要在BST中找到节点的值等于`val`的节点node。 返回以该节点node开始的subtree。 如果节点不存在，则返回 NULL。

例：

![](../../.gitbook/assets/tree1%20%281%29.jpg)

Input: `root = [4,2,7,1,3], val = 2`   
Output: `[2,1,3]`



### 算法：Recursion

如果根节点root为null，返回root（null）；

如果根节点root的值等于搜索值val，返回root；`root.val == val`

如果 val &lt; root.val，进入根节点的左子树left subtree查找；`searchBST(root.left, val)`

如果 val &gt; root.val，进入根节点的右子树right subtree查找；`searchBST(root.right, val)`

```text
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        TreeNode res = new TreeNode();
        if (root == null) return null;
        
        if (root.val == val) {
            res = root;
            return res;
        }
        
        if (root.val > val) {
            res = searchBST(root.left, val);
        } else {
            res = searchBST(root.right, val);
        }
        
        return res;
    }
}
```

上面的好理解，下面的更简洁：

```text
class Solution {
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null) return null;
        
        if (root.val == val) {
            return root;
        }
        
        if (root.val > val) {
            return searchBST(root.left, val); //可以直接return
        } else {
            return searchBST(root.right, val); //下面结尾就不需要再return
        }
        
    }
}
```

Time：平均时间是`O(logn)`，也就是树的高度，最坏的情况是`O(n)`； height of the tree  
Space：平均时间是`O(logn)`，也就是树的高度，最坏的情况是`O(n)`；



