---
description: Two pointer
---

# \[Leetcode\]11. Container With Most Water

原题地址：[https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/) 关键词：Two pointer

题意：盛最多水的容器。  
给个坐标，在坐标内画 n 条垂直线 。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水。返回最多的那个水的容量。

例子：

![](../.gitbook/assets/question_11.jpg)

Input: `height = [1,8,6,2,5,4,8,3,7]`   
Output: `49`   
Explanation: 图中垂直线代表输入数组 \[1,8,6,2,5,4,8,3,7\]。在此情况下，容器能够容纳水的最大值为 49。



### 方法1：Brute force

两层for loop，找出所有容器，返回最大的。时间`O(n ^2)`，耗时太久。



### 方法2：Two pointer



```text
class Solution {
    public int maxArea(int[] height) {
        int res = 0;
        int curArea = 0;
        int left = 0;
        int right = height.length - 1;
        
        while (left < right) {
            curArea = Math.min(height[left], height[right]) * (right - left);
            res = Math.max(res, curArea);
            
            if (height[left] < height[right]) {
                left++;
            } else {
                right--;
            }
        }
        
        
        return res;
    }
}
```

Time: O\(n\)；  
Space: O\(1\)；







