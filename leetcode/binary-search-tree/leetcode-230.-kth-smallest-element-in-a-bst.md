---
description: 'Binary Search Tree, BST'
---

# \[Leetcode\]230. Kth Smallest Element in a BST

原题地址：[https://leetcode.com/problems/kth-smallest-element-in-a-bst/](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) 关键词：Binary Search Tree, BST

题意：返回BST中第K小的元素。  
给一个Binary Search Tree，返回val第K小的元素，从 1 开始计数。



### 算法：中序遍历 Inorder Traversal

把所有的node的val放进一个ArrayList。如果用Inorder Traversal，那么这个list自然就是sorted。然后直接返回第k - 1个元素即可。

```text
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        if (root == null) return 0;
        List<Integer> res = new ArrayList<>();
        
        dfs(root, res);
        
        return res.get(k - 1);
    }
    
    // in-order
    private void dfs(TreeNode root, List<Integer> res) {
        if (root == null) return;
        
        dfs(root.left, res);
        
        res.add(root.val);
        
        dfs(root.right, res);
        
    }
}
```

Time: `O(n)`；  
Space: `O(n)`；list的size





