---
description: queue
---

# \[Leetcode\]566. Reshape the Matrix

原题地址：[https://leetcode.com/problems/reshape-the-matrix/](https://leetcode.com/problems/reshape-the-matrix/) 关键词：queue

题意：给一个matrix，重新变换长宽，把所有元素按顺序放进新的matrix；

例：

![](.gitbook/assets/reshape1-grid.jpg)

Input: `mat = [[1,2],[3,4]], r = 1, c = 4`   
Output: `[[1,2,3,4]]`

### 方法1：queue

算法：把所有元素装进queue，然后依次放入新的matrix

```text
class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length) {
            return nums;
        }
        
        Queue<Integer> queue = new LinkedList();
        
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                queue.offer(nums[i][j]);
            }
        }
        
        for (int i = 0; i < r; i++) {
            for (int j = 0; j < c; j++) {
                res[i][j] = queue.poll();
            }
        }
        
        return res;
    }
}
```

Time complexity：O\(m⋅n\)；m、n为长宽  
Space complexity：O\(m⋅n\)



### 方法2：Space optimal

算法：就在给出的matrix上操作。只需遍历一次，rows和cols为新的长宽，每加上一个新元素就`cols++`，当`cols == c`的时候就进入下一行（下一个row），进入下一行的方法：`rows++`；

```text
public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int[][] res = new int[r][c];
        if (nums.length == 0 || r * c != nums.length * nums[0].length)
            return nums;
        
        int rows = 0, cols = 0;
        
        for (int i = 0; i < nums.length; i++) {
            for (int j = 0; j < nums[0].length; j++) {
                res[rows][cols] = nums[i][j];
                cols++;
                if (cols == c) {
                    rows++;
                    cols = 0;
                }
            }
        }
        
        return res;
    }
}
```

Time complexity：O\(m⋅n\)；m、n为长宽  
Space complexity：O\(m⋅n\)

