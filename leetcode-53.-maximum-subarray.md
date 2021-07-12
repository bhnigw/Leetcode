---
description: 'DP, Dynamic programing, Kadane Algorithm'
---

# \[Leetcode\]53. Maximum Subarray

原题地址：[https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/) 关键词：DP, Dynamic programing, Kadane Algorithm

题意：给一个数组 nums ，找和最大的subArray；

Example 1:  
`Input: nums = [-2,1,-3,4,-1,2,1,-5,4]   
Output: 6`Explanation: \[4,-1,2,1\] has the largest sum = 6.   
Example 2:  
`Input: nums = [-1]   
Output: -1`

### 方法1：Dynamic Programing

`nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4];`

  `DP = [-2, 1, -2, 4,  3, 5, 6,  1, 5];`

```text
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int[] DP = new int[nums.length];
        
        DP[0] = nums[0];
        
        // 构造DP数列
        for (int i = 1; i < nums.length; i++) {
            if (DP[i - 1] < 0) {
                DP[i] = nums[i];
            } else {
                DP[i] = DP[i - 1] + nums[i];
            }        
        }
        
        // 在DP[]中找最大
        int res = DP[0];
        for (int i : DP) {
            res = Math.max(i, res);
        }
        
        return res;
    }
}
```

### 方法2：优化

第5行初始化res的时候为什么不能是0？  
因为如果input是`nums = [-1]`，第15行会输出0，是错误的；结果应该是-1；

```text
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int res = Integer.MIN_VALUE; //这里不能是0
        int currMax = 0;
        
        for (int i = 0; i < nums.length; i++) {
            if (currMax < 0) {
                currMax = nums[i];
            } else {
                currMax += nums[i];
            }
            
            res = Math.max(res, currMax);
        }
        
        
        return res;
    }
}
```

Time complexity: O\(N\), where N is the length of `nums`.

Space complexity: O\(1\)

