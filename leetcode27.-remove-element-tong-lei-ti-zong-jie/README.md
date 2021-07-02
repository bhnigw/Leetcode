# \[Leetcode\]27. Remove Element\(同类题总结\)

原题地址：[https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/) 

题意：

要求做到Space Optimal，不能另外创建新数组，只能在原数组上操作；

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

