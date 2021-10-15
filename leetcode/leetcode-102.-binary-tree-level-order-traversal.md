---
description: Tree，Level Order Traversal
---

# \[Leetcode]★102. Binary Tree Level Order Traversal

原题地址：[https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/) 关键词：Tree，Level Order Traversal

题意：二叉树的**层序遍历（**Level Order Traversal）\
题目给一个tree，把tree每一层的值分别放入二维list里并返回；

例：

![](../.gitbook/assets/tree1.jpg)

Input: root = `[3,9,20,null,null,15,7] `\
Output: `[[3],[9,20],[15,7]]`



### 方法1：BFS

层序遍历就是把二叉树分层，然后每一层从左到右遍历；

![](../.gitbook/assets/ce41cf1cabfa7a56387f63d927c8819fe1479ecf6f193a2a1b47964f5a8d1c8e.jpg)

乍一看，我们可以直接用一个Queue然后 BFS 得出层序遍历结果。然而，BFS 的遍历结果是个一维数组，我们**无法区分Queue中的结点来自哪一层**。而题目的层序遍历要求我们区分每一层，也就是返回一个二维数组：

![](<../.gitbook/assets/fd1d63037d0e2f787d2140fee406e109094a4f66ab0837a7273f8b371eef8096 (1).jpg>)

那问题就来了！怎样区分每一层的node，然后分层放进二维数组呢？？？这也是这道题的重点！

我们需要在每一层while循环开始时，记录当前queue的长度n，也就是每一层的size，然后在while里用for循环`(int i = 0; i < size; i++)`把这一层的node都poll光

![](../.gitbook/assets/IMG\_6425.jpg)

最终代码：

```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int size = queue.size(); //记录当前queue的大小，也就是每一层的size
            List<Integer> curLevel = new ArrayList<>();
            
            for (int i = 0; i < size; i++) {
                TreeNode curNode = queue.poll(); //这for循环会把这一层的node都poll光！
                curLevel.add(curNode.val);       //每poll一个把值加入当前的小list
                
                if (curNode.left != null) {
                    queue.offer(curNode.left);
                }
                if (curNode.right != null) {
                    queue.offer(curNode.right); //把下一层的node全部加进来！
                }
            }            
            
            res.add(curLevel); //把每一层的list加入res
        }
        
        return res;
    }
}
```

Time: `O(N)`，每个node走了一遍\
Space: `O(N)`，queue的size 



### 方法2：DFS

按照DFS的步骤，会先访问节点 `1`、`2`、`3`；然后节点`4`，最后是`5`、`6`。

![](../.gitbook/assets/aeed09e12573ec00d83663bb4f77562e8904ac58cdb2cbe6e995f2ac33b12934-0203\_1.gif)

那问题又来了！怎样确定节点来自哪一层呢？？

我们需要在每次recursion的时候，带一个整数level进去，表示当前的层数；每进入下一层，层数level就加1；并且在每一层level开始的时候初始化new一个ArrayList；

```
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        if (root == null) return res;
        
        int level = 0;
        helper(root, level, res);
        
        return res;
    }
    
    private void helper(TreeNode root, int level, List<List<Integer>> res) {
        if (res.size() == level) { // 注意什么意思
            res.add(new ArrayList<Integer>());
        }
        
        res.get(level).add(root.val);
        
        if (root.left != null) {
            helper(root.left, level + 1, res); // 不能是++level（重点）
        }
        
        if (root.right != null) {
            helper(root.right, level + 1, res);// 如果是++level那么它记录的就是node的总个数而不是层数
        }
    }
}
```

#### 要注意的地方：

第13行本来的意思是，如果res里面没有还这一层的元素，就new一个list来装本层的元素；为什么不能用`if (res.get(i) != null)`呢？因为当位置i没有元素时，ArrayList会报错IndexOutOfBoundsException；所以只能用res的size来判断，当level在第0层也就是根节点root的时候，size也为0；14行时res的size变为1，下面的dfs进入level 1的时候是全新的一层；

意思就是，每当`res.size() == level`的时候，**说明进入了全新的一个level**，那么就为本层new一个ArrayList；那么问题就来了，怎样保证recursion的时候把同一层的加到同一个list里且不会new多余的list呢？下面就要注意level的用法：

我们要保证DFS每前进一步，层数level要加1，同时要**保持回来的时候level的值在本层保持不变**！所以第20行用`level + 1`而不是`++level`；`level + 1`不会改变level本身的值，而`++level`会让level本身的值加1；

`level + 1`可以保证在DFS每一层的时候，同一层的level值不变。能把同一层的node加到同样的list里面去。

如果是`level + 1`，记录的是层数，             会输出：`[[1], [2, 5], [3, 4, 6]]` ✅\
如果是`++level`，记录的是node的总个数，会输出：`[[1], [2], [3], [4], [5], [6]]` ❌

举例：比如在dfs到第二层node = 5的位置时，进入到helper()后，level值为1，res的size是3，所以第13行不会new多余的list。

### 更好理解的方式：

![](../.gitbook/assets/IMG\_6435.jpg)

所以level与node个数无关，只与树的高度有关；



Time: `O(N)`，每个node走了一遍\
Space: `O(h)`；h是树的高度，也就等于是recursive的层数；



### 本题要记住的重点：

怎样确定BFS和DFS中的结点来自哪一层。

