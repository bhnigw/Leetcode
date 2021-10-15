---
description: Binary Search
---

# \[Leetcode]162. Find Peak Element

原题地址：[https://leetcode.com/problems/find-peak-element/](https://leetcode.com/problems/find-peak-element/) 关键词：Binary Search

题意：寻找数组的峰值；\
给一个数组 `nums[]`，找到峰值元素并返回其index，峰值是指其值大于左右相邻值的元素。数组可能包含多个峰值，返回任何一个即可。



### 方法1：Linear Scan； O(n) Time （不推荐）

峰值出现的情景：区间一直单调递增，然后开始单调递减；\
也就是说，只要**找到第一个开始单调递减的元素**，那么它的前一个元素就是峰值。

```
public class Solution {
    public int findPeakElement(int[] nums) {
        for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] > nums[i + 1]) { //当前元素比下一个大，说明开始单调递减
                return i;
            }
        }
        return nums.length - 1; //如果一直递增就返回最后一个index
    }
}
```

Time: O(n)；\
Space: O(1)；



### 方法2：Binary Search； O(logn) Time

峰值出现的情景：区间一直单调递增，然后开始单调递减；也就是说，只要朝着单调递增的区间一直往上走，那么顺着一路下去一定能找到峰值。

在题目描述中出现了`nums[-1] = nums[n] = -∞`，这就代表着，只要数组中存在一个元素比相邻元素大，那么沿着它一定可以找到一个峰值。

根据左右指针计算中间位置mid，**并比较`mid`与`mid+1`的值**：\
如果`mid`更大，说明峰值在左边，舍弃掉右边：right = mid；\
如果`mid + 1`更大，说明峰值在右边，舍弃掉左边：left = mid+ 1；

```
class Solution {
    public int findPeakElement(int[] nums) {
        if (nums == null || nums.length == 0) return 0;
        
        int res = 0;
        int left = 0, right = nums.length - 1;
        
        while (left < right) {
            int mid = left + (right - left) / 2; //防止溢出
            
            if (nums[mid] > nums[mid + 1]) { //注意比的是什么
                right = mid;
            } else {
                left = mid + 1;
            }
        }
        
        return left;
    }
}
```

Time: O(logn)；\
Space: O(1)；





