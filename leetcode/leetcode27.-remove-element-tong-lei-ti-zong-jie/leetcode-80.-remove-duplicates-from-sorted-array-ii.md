---
description: Two pointer
---

# \[Leetcode]80. Remove Duplicates from Sorted Array II

原题地址：[https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) 关键词：Two pointer

题意：去除数组中重复超过两次的数；\
已经sorted数组`nums[]`中，如果一个数重复出现超过两次，就剔除掉多余的，只让它出现两次；\
返回：去除重复后数组左边的长度length；\
（要求做到Space Optimal，不能另外创建新数组，只能在原数组上操作）

Input: `nums = [0, 0, 1, 1, 1, 1, 2, 3, 3] `\
Output: 7, `nums = [0, 0, 1, 1, 2, 3, 3, _, _]`



### 此类题统一思路模板：

1. 用指针reserve去reserve有效起始位置，同时要确定：满足什么样的条件才能占据这个位置；
2. 用第二个指针`i`去遍历给定数组nums的每一个元素；
3. 一旦当前指针`i`扫到的元素`nums[i]`满足reserve位置的要求，那么就赋值`nums[reserve] = nums[i]`；



### 将模板代入本题算法：

●**reserve起始位置：**第三个数(index 2)；\
为什么从第三个数字开始？因为题目要求同样的数至多允许出现两次，所以即便前两个数一样，也一定满足至多出现两次的要求；所以我们从第三个数字开始扫描；

●**需要满足的条件：**同一个数至多出现2次；\
如何检查？只要指数`i`对应的数，与`reserve - 2`对应的数相等，则表明同一个数字出现了3次；\
❗️为什么这么说？\
因为这是一个sorted的数组，那么若指数`i`对应的数，与`reserve - 2`对应的数相等 ⇒ 则也一定等于`reserve - 1 ` ⇒ 则同一个数重复出现三次 ⇒ 则不合条件！！

若满足条件，就赋值`nums[reserve] = nums[i]`，然后`reserve++`；

详细图解：

![](../../.gitbook/assets/IMG\_6380.jpg)



![](../../.gitbook/assets/IMG\_6381.jpg)

```
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

代码结构：\
1\. 初始化reserve的值；\
2\. for循环\
3\. 判断if，如果满足就`nums[reserve] = nums[i]`然后reserve++；

Time: O(n);\
Space: O(1);



注意一定要理清：

1. 指针reserve的责任，和初始值；
2. 指针i的责任，和初始值；
3. 什么条件下，`nums[reserve] = nums[i]`
