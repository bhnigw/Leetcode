---
description: Two pointer
---

# \[Leetcode\]80. Remove Duplicates from Sorted Array II

原题地址：[https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) 关键词：Two pointer





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

