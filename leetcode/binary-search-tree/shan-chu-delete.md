---
description: Binary Search Tree
---

# ★删除 Delete

原题地址：[https://leetcode.com/problems/delete-node-in-a-bst/](https://leetcode.com/problems/delete-node-in-a-bst/) 关键词：Binary Search Tree

题意：删除BST上值为`key`的node，返回整个tree；



### 算法：Recursion

如果没找到删除的节点，直接返回null；

当找到要删除的节点时`key == root.val`，有以下4种情况：

● **节点情况1：**没有左child，也没有右child，也就是**Leaf节点**，则直接删除它：`return null`

![](../../.gitbook/assets/IMG\_6436.jpg)

****\
****● **节点情况2：**只有左child（只有left subtree）：直接`return left subtree `

![](../../.gitbook/assets/IMG\_6437.jpg)

****\
****● **节点情况3：**只有右child（只有right subtree）：直接`return right subtree `

![](../../.gitbook/assets/IMG\_6438.jpg)

****\
****● **节点情况4：**既有左child，又有右child。设当前要删除的节点为`cur_node`，找到它的**right** subtree中**值最小的节点**`min_node`，把`min_node.val`赋值给`cur_node.val`；然后删掉right subtree的这个`min_node`：进行recursion，继续找`min_node`的right subtree中值最小的节点`min_min_node`，继续替换继续找...

![](../../.gitbook/assets/del_succ.png)



所以，具体算法为：

* 如果`key > root.val`，说明要删除的节点在右子树，root.right = deleteNode(root.right, key)；
* 如果`key < root.val`，说明要删除的节点在左子树，root.left = deleteNode(root.left, key)；
* 如果`key == root.val`，则该节点就是我们要删除的节点，则： 
  * 如果该节点是Leaf节点，则直接删除它：`root = null`；
  * 如果该节点只有左child，。 
  * 如果该节点只有右child，。 
  * 如果该节点左右都有child，找到它right subtree中值最小的节点，替换val；然后用recursion删掉right subtree的这个最小的节点...
* 返回 root。

```
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return root;
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else {
            root.right = deleteNode(root.right, key);
        }
        
        if (key == root.val) {
            if (root.left == null && root.right == null) {       // 情况1，Leaf节点
                return null;
            } else if (root.left != null && root.right == null) { // 情况2，有左child
                root = root.left;
            } else if (root.left == null && root.right != null) { // 情况3，有右child
                root = root.right;
            } else {                                              // 情况4，左右都有child
                TreeNode minNode = findMinNode(root.right);
                root.val = minNode.val;                         // 把root的值替换为minNode的值
                
                root.right = deleteNode(root.right, minNode.val); // 删去minNode
            }
        }
        
        return root;  
    }
    
    private TreeNode findMinNode(TreeNode root) {
        while (root.left != null) { // 最小的一定出现在左边
            root = root.left;       //所以顺着左边一路找下去
        }
        
        return root;
    }
}
```

Time：`O(H)`，H是树的高度，height of the tree，高度H平均值是`logn`，在worst case情况下是`n`；\
Space：`O(H)`



### 要记住的重点：

怎样在Binary Search Tree找最小的node；\
怎样在Binary Search Tree找最大的node；



