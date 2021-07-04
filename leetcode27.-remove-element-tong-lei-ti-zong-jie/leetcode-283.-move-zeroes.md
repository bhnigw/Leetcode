---
description: Two pointer
---

# \[Leetcode\]283. Move Zeroes

原题地址：[https://leetcode.com/problems/move-zeroes/](https://leetcode.com/problems/move-zeroes/) 关键词：Two pointer

题意：一个整数array，把所有的0移到右边，其余数左移且顺序不变  
`Input: nums = [0,1,0,3,12]   
Output: [1,3,12,0,0]`  
（要求做到Space Optimal，不能另外创建新数组，只能在原数组上操作）



算法：

1. 先设置一个reserve 为0作为起始index；
2. 第一次遍历数组，遇到不是0的，就依次放在数组最左边 `nums[reserve] = 非零数;`然后reserve++；
3. 第一次遍历完后，此时reserve为数组改动后所有非零数的右边一位的index，从这reserve开始往后就应该全部为0；
4. 第二次遍历数组，从reserve开始到末尾，全部赋值0即可；

```text
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) return; //null check
        
        int reserve = 0;
        
        for (int i = 0; i < nums.length; i++) { //不为0的挨个排到原数组左边 
            if (nums[i] != 0) {
                nums[reserve] = nums[i];
                reserve++;
            }
        }
        
        for (int i = reserve; i < nums.length; i++) { //指数reserve右边全部填上0
            nums[i] = 0;
        }
    }
}
```

Time: O\(n\);  
Space: O\(1\);

