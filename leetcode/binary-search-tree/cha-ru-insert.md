---
description: Binary Search Tree
---

# 插入 Insert

原题地址：[https://leetcode.com/problems/insert-into-a-binary-search-tree/](https://leetcode.com/problems/insert-into-a-binary-search-tree/) 关键词：Binary Search Tree



```text
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

