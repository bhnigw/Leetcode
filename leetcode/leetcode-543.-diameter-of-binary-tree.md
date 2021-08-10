# \[Leetcode\]543. Diameter of Binary Tree

求Maximum Path Length





观察下面为什么有错：

```text
// 错误代码
class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        int res = 0;
        if (root == null) return res;
        
        res = dfs(root, res);
        
        return res;
    }
    
    private int dfs(TreeNode root, int res) {
        if (root == null) return 0;
        int leftLength = 0;
        int rightLength = 0;
        
        leftLength = dfs(root.left, res);
        rightLength = dfs(root.right, res);
        
        res = Math.max(leftLength + rightLength, res);
        
        return Math.max(leftLength, rightLength) + 1;
    }
}
```



正确代码：

```text
class Solution {
    public int diameterOfBinaryTree(TreeNode root) {
        int[] res = new int[1];
        if (root == null) return res[0];
        
        dfs(root, res);
        
        return res[0];
    }
    
    private int dfs(TreeNode root, int[] res) {
        if (root == null) return 0;
        
        int leftLength = dfs(root.left, res);
        int rightLength = dfs(root.right, res);
        
        res[0] = Math.max(leftLength + rightLength, res[0]);
        
        return Math.max(leftLength, rightLength) + 1;
    }
}
```



