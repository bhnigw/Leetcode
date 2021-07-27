# 查找 Search

原题地址：[https://leetcode.com/problems/search-in-a-binary-search-tree/](https://leetcode.com/problems/search-in-a-binary-search-tree/)





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
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
        
    }
}
```



