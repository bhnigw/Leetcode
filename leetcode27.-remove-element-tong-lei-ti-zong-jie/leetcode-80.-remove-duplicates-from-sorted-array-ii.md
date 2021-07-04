---
description: Two pointer
---

# \[Leetcode\]80. Remove Duplicates from Sorted Array II

原题地址：[https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) 关键词：Two pointer

题意：去除数组中重复超过两次的数；  
已经sorted数组`nums[]`中，如果一个数重复出现超过两次，就剔除掉多余的，只让它出现两次；  
返回：去除重复后数组左边的长度length；  
（要求做到Space Optimal，不能另外创建新数组，只能在原数组上操作）

Input: `nums = [0, 0, 1, 1, 1, 1, 2, 3, 3]`   
Output: 7, `nums = [0, 0, 1, 1, 2, 3, 3, _, _]`



```text
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int reserve = 2;
        
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] != nums[reserve - 2]) { //注意
                nums[reserve] = nums[i];
                reserve++;
            }
        }
        
        return reserve;
    }
}
```

Time: O\(n\);  
Space: O\(1\);

