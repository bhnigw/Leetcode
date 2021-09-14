# \[Leetcode\]572. Subtree of Another Tree

原题地址：[https://leetcode.com/problems/subtree-of-another-tree/](https://leetcode.com/problems/subtree-of-another-tree/)

题意：判断是不是Subtree。  
给两棵二叉树`root`和`subRoot`。检验`root`中是否包含`subRoot`。如果存在，返回 true，否则返回 false 。两棵树完全相同也可以看做一棵树是另一棵树的子树。

例：

![](../.gitbook/assets/subtree1-tree.jpg)

Input: `root = [3,4,5,1,2], subRoot = [4,1,2]`  
Output: true



### 算法：Recursion

**核心思想：**对tree进行recursion，只要探测到任何一个子树，与input给的subRoot完全相同，那么就返回true；（两棵树完全相同也可以看做一棵树是另一棵树的子树）

算法不复杂可以直接看代码；本题需要记住的重点：怎样避免nullPointerException❓

#### 在主方法里：

* 当`subRoot`为null，则返回true；因为null是所有树的子树；
* 当`subRoot`不为null，只要`root`为null肯定不是子树；
* 如果两棵树完全相同返回true；
* 探测到任何一个子树，与input给的subRoot完全相同，那么就返回true；

#### 在判断两棵树是否相同时：

* 如果两个node同时为null，算是相同的树，返回true；
* 如果只有一个为null则不是相同的树；
* 任何一个节点的val不同则不是相同的树；



（[一个小知识点](https://bhnigw.gitbook.io/-1/shu-ju-jie-gou-map#ru-guo-ba-treenode-jia-ru-hashmap)）

```text
class Solution {
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if (subRoot == null) return true; // subRoot为null一定都是true
        if (root == null) return false;  // 这里subRoot一定不为null, 只要root为null肯定是false
        
        if (isSameTree(root, subRoot)) return true; // 如果两棵树完全相同返回true
        
        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot); 
    
    // 判断两棵树是否相同
    private boolean isSameTree(TreeNode root1, TreeNode root2) {
        if (root1 == null && root2 == null) return true; // 两个都为null则是相同的树，返回true
        if (root1 == null || root2 == null) return false; // 只有一个为null则不是相同的树
        
        if (root1.val != root2.val) return false; // 任何一个节点的val不同则不是相同的树

        return isSameTree(root1.left, root2.left) && isSameTree(root1.right, root2.right);
    }
}
```

Time: `O(M * N)`；  
解释：M和N分别是`root`和`subRoot`的节点总数，对于每一个`root`上的点，都需要做一次DFS来和`subRoot`匹配，匹配一次的时间代价是`O(N)`，那么总的时间代价就是`O(M * N)`

Space: `O(max(H1, H2))`；  
解释：H1是`root`的深度，H2是`subRoot`的深度；为什么不直接是H1，因为input给出的`subRoot`深度有可能会比root大。



相关题目：





