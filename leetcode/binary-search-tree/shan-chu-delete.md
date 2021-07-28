---
description: Binary Search Tree
---

# ★删除 Delete

原题地址：[https://leetcode.com/problems/delete-node-in-a-bst/](https://leetcode.com/problems/delete-node-in-a-bst/) 关键词：Binary Search Tree

题意：删除BST上值为val的node，返回整个tree；

### 算法：Recursion

没找到删除的节点，遍历到空节点直接返回；

当找到要删除的节点时，有以下4种情况：

**节点情况1：**没有左child，也没有右child，也就是Leaf节点，则直接删除它：`root = null`；

![](../../.gitbook/assets/del_leaf.png)

  
**节点情况2：**只有左child（只有left subtree）return the left subtree 

**节点情况3：**只有右child（只有right subtree）return the right subtree 

**节点情况4：**既有左child，又有右child。找到它右边子树中最小的节点find the minimum value in the right subtree, set that value to the currently found node, then recursively delete the minimum value in the right subtree



![](../../.gitbook/assets/del_succ.png)

  
****

node doesn't have left or right - return null 

node only has left subtree- return the left subtree 

node only has right subtree- return the right subtree 

node has both left and right - find the minimum value in the right subtree, set that value to the currently found node, then recursively delete the minimum value in the right subtree

所以，具体算法为：

* 如果`key > root.val`，说明要删除的节点在右子树，root.right = deleteNode\(root.right, key\)；
* 如果`key < root.val`，说明要删除的节点在左子树，root.left = deleteNode\(root.left, key\)；
* 如果`key == root.val`，则该节点就是我们要删除的节点，则： 
  * 如果该节点是Leaf节点，则直接删除它：`root = null`；
  * 如果该节点不是Leaf节点，且有右child，则用它的后继节点的值替代：`root.val = successor.val`，然后删除后继节点successor。 
  * 如果该节点不是Leaf节点，且**只**有左child，则用它的前驱节点的值替代：`root.val = predecessor.val`，然后删除前驱节点predecessor。 
* 返回 root。







