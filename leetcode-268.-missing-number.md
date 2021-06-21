---
description: 'Array, HashSet, 数学技巧'
---

# \[Leetcode\]268. Missing Number

原题地址：[https://leetcode.com/problems/missing-number/](https://leetcode.com/problems/missing-number/) 关键词：Array, HashSet, 数学技巧

题意：数组长度为n（包含n个数），每个数都不同，且范围在 \[0, n\] ，找出 \[0, n\] 这个范围内没有出现在数组中的那个数。要求：Time: O\(n\)；Space: O\(1\).

方法一：Sorting；Time: O\(nlogn\)；Space: O\(1\)；

方法二：Hash Set；先把nums所有数放进set，然后从0到n检查set.contains\(number\)，如果遇到没有contain的就返回这个数。Time: O\(n\)；Space: O\(n\).

方法三：数学技巧，高斯求和，Gauss Sum；由条件知，只需由 **高斯求和公式所得** 减去 **数组本身的和**，即可求得缺失的数。（需要死记硬背）

```text
class Solution {
    public int missingNumber(int[] nums) {
        //Gauss sum
        int GaussSum = (1 + nums.length) * nums.length / 2;
        
        //Array sum
        int ArraySum = 0;
        for (int num : nums) {
            ArraySum += num;
        }
        
        return GaussSum - ArraySum;
    }
}
```

Time: O\(n\)  
Space: O\(1\)

