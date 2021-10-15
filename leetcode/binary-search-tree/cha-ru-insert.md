---
description: Binary Search Tree
---

# 插入 Insert

原题地址：[https://leetcode.com/problems/insert-into-a-binary-search-tree/](https://leetcode.com/problems/insert-into-a-binary-search-tree/) 关键词：Binary Search Tree

题意：向BST插入一个值为val的node，返回整个tree；

![](<../../.gitbook/assets/insertbst (1).jpg>)

Input: `root = [4,2,7,1,3], val = 5 `\
Output: `[4,2,7,1,3,5] `有多种解，返回一种即可



### 算法：Recursion

如果根节点root为null，要插入的node就是整个tree，直接new一个TreeNode然后返回；`return new TreeNode(val);`

根据Binary Search Tree特性，当val值小于节点node值时，插入位置在左侧树；相反，当val值大于节点node值时，插入位置在右侧树。

```
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) {
            return new TreeNode(val);
        }
        
        if (root.val > val) {
            root.left =  insertIntoBST(root.left, val);
        } else {
            root.right =  insertIntoBST(root.right, val);
        }
        
        return root;
    }
}
```

Time：平均时间是`O(logn)`，也就是树的高度，最坏的情况是`O(n)`； height of the tree\
Space：平均时间是`O(logn)`，也就是树的高度，最坏的情况是`O(n)`；
