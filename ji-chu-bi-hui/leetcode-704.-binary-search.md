---
description: Binary Search
---

# \[Leetcode\]704. Binary Search

原题地址：[https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/) 关键词：Binary Search

题意：给一个sorted数组nums，给一个target number，找出它在nums中的位置index，如果不存在则返回-1。

算法：Binary Search；每次劈半。用以下方法，返回left和right都一样。

```text
class Solution {
    public int search(int[] nums, int target) {
        
        //range of binary search
        int left = 0;
        int right = nums.length - 1;
        
        //binary search
        while (left < right) {
            int mid = left + (right - left) / 2; //防止溢出
            
            if (nums[mid] >= target) { 
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        //如果能保证解一定存在，就不用check，否则要check一下
        return nums[right] == target ? right : -1; 
    }
}
```

**Time: O\(logn\);**  
Space: O\(1\);

注意：  
1. 上面`left < right` 无等号，下面`nums[mid] >= target` 有等号；  
2. mid注意防止溢出；  
**3. return的时候，返回`left`或者`right`都可以，结果都是一样。**

