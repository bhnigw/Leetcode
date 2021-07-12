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

算法：

把“**到nums里每一个index为止的最大的subArray和**“的具体数值算出来，放到`DP[]`里；  
`DP[]`此时代表的意义：“**到nums里每一个index为止的最大的subArray和**“

计算的规则是怎样呢？？  
对于当前位置的指数`i`，如果前一个的`DP[i - 1]`小于0，说明nums里到`i - 1`为止，最大子集的和为负数，如果此刻`nums[i]`加上一个负数，是没有任何帮助的；所以舍弃掉nums里到`i - 1`为止的所有数字，只留下`nums[i]`。最后我们把`nums[i]`的值赋给`DP[i]`，意味着：nums里到`i`为止的最大子集之和就是`nums[i]`本身。

如果前一个的`DP[i - 1]`大于0，说明nums里到`i - 1`为止，最大子集的和为正数，如果此刻`nums[i]`加上一个正数，无论`nums[i]`的值本身是多少，都会变大，都是有帮助的；所以我们把`nums[i]`和`DP[i - 1]`两数相加之和赋给`DP[i]`；



实例：  
`nums = [-2, 1, -3, 4, -1, 2, 1, -5, 4];`

  `DP = [-2, 1, -2, 4, 3 , 5, 6, 1 , 5];`

解释：

`DP[2] = -2`的意思就是：到`nums[]`的index = 2为止，最大的sub array和为 - 2，此时最大的sub array是`{1, -3}`；

`DP[3] = 4`的意思就是：到`nums[]`的index = 3为止，最大的sub array和为4，此时最大的sub array是`{4}`；（因为`DP[2]`小于0，加上它毫无帮助，所以舍弃它）

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

```text
// 此方法也可
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int res = nums[0];
        int currMax = res;
        
        for (int i = 1; i < nums.length; i++) { //从1开始
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

