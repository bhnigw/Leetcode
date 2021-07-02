---
description: Two pointer
---

# \[Leetcode\]27. Remove Element\(同类题总结\)

原题地址：[https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/) 关键词：Two pointer

题意：在一个unsorted数组`nums[]`中，给一个整数val，去除`nums[]`中所有等于val的数字，并把其他所有不等于val的数字依次放到数组最左边，右边不用管；  
返回：去除val后数组左边的长度length；  
（要求做到Space Optimal，不能另外创建新数组，只能在原数组上操作）

例：  
Input: `nums = [0, 1, 2, 2, 3, 0, 4, 2], val = 2`   
Output: `5, nums = [0, 1, 3, 0, 4, _, _, _]`   
解释：去除掉数组所有等于2的数之后，数组左边的有效长度为5



```text
class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums == null || nums.length == 0) return 0;
        
        int reserve = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
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

