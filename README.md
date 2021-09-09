---
description: Binary Search
---

# Binary Search

原题地址：[https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/) 关键词：Binary Search

题意：给一个sorted数组`nums[]`，给一个整数`target`，找出它在nums中的位置index，如果不存在则返回`-1`。

### 算法：Binary Search；每次劈半

记住，if中等号判断交给right，下面返回right

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

**Time: O\(logn\);** Space: O\(1\);



### ❗️注意：

if条件中，=等于的判断，只能交给right！为什么呢？（或者说`mid + 1`这个东西，只能赋给left，不能把right赋成`mid - 1`）

```text
 // 错误代码 Time Limit Exceeded
 private int binarySearch(int left, int right, int[] nums, int target) {
    while (left < right) {
        int mid = left + (right - left) / 2; //错误的根源
            
        if (nums[mid] <= target) {
            left = mid;          //错误的出现
        } else {
            right = mid - 1;
        }
    }
        
    return nums[left] == target ? left : -1;
}
```

上面的代码，如果input是`[1, 2]`, `target = 3`，那么起始left会指向1，mid也会指向1，right会指向2，经过第6行的if判断后，left和mid的值依然是1保持不变，while就会陷入死循环。错误的来源是什么？是因为第4行，使用"/"进行division的时候1/2的值为0，所以left和mid的值会永远不变，永远相等。

修正后的代码：

```text
private int binarySearch(int left, int right, int[] nums, int target) {
    while (left < right) {
        int mid = left + (right - left) / 2;
            
        if (target > nums[mid]) {
            left = mid + 1;
        } else {
            right = mid;
        }
    }
        
    return nums[right] == target ? right : -1; //只能返回right，因为如果input是[1]，
                                               //那么left会indexOutOfBound  
}
```



### 要记住的重点：

1. 上面`left < right` 无等号，下面if判断中，=等号只能交给`right`；  
2. mid注意防止溢出；  
**3. return的时候，只能返回`right`。**

简便记忆：if中等号判断交给right，下面返回right，**什么都是right，统统都是right！**



其他例题：

{% page-ref page="leetcode/leetcode-162.-find-peak-element.md" %}

{% page-ref page="leetcode/leetcode-33.-search-in-rotated-sorted-array.md" %}







