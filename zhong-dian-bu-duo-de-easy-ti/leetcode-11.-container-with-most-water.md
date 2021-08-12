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

初始化两个指针left和right，分别指向头和尾。

由木桶效应可知，决定蓄水量的，是那个最短的木板。所以：  
`蓄水量` = `left和right最短高度` × `left到right的距离`

**指针移动规则：**把木板更矮的那一个指针，向中间方向移动一位。

为什么❓

因为如果移动木板更高的那个指针，那么上面公式里前者`left和right最短高度`不会增加，后者`left到right的距离`会减小，那么这个乘积会减小。因此，我们移动木板更高的那个指针是不合理的。因此，我们移动木板更矮的那个指针。



为什么木板更矮的那个指针不可能再作为容器的边界了❓

假设当前`left`指针和`right`指针指向的木板高度别为`x`和`y`，两个指针之间的距离为dis。那么，它们组成的容器的容量为：

`min(x, y) * dis`；假设x更小，结果就等于`x * dis`

如果保持`left`指针的位置不变，它始终为短板！那么无论`right`指针在哪里，这个容器的容量都不会超过`x * dis`。  
也就是说，无论我们怎么移动`right`指针，得到的容器的容量都小于移动前容器的容量。所以，我们可以丢弃`left`指针的木板，然后将向右移动一个位置，此时新的`left`指针，与原先的`right`指针的位置，才可能会作为容器的新边界。

一句话总结：我们每次向内移动短板，所有的状态都**不会导致丢失面积最大值** 。

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







