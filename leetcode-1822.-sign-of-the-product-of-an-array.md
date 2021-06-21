---
description: 数学技巧
---

# \[Leetcode\]1822. Sign of the Product of an Array

原题地址：[https://leetcode.com/problems/sign-of-the-product-of-an-array/](https://leetcode.com/problems/sign-of-the-product-of-an-array/) 关键词：数学技巧

题意：给个数组nums，把里面所有数相乘，结果为正数返回1，为负数返回-1，为零则返回0。



方法一：数负数的个数，个数为偶数even则返回1，为奇数odd就返回-1；有零直接返回0

```text
class Solution {
    public int arraySign(int[] nums) {
        
        int count = 0;
        
        for (int num : nums) {
            if (num == 0) return 0;       
            if (num < 0) count++;
        }
        
        return count % 2 == 0 ? 1 : -1;  //注意如何判断奇偶
    }
}
```



方法二：初始一个整数sign赋值1，遍历nums，遇到一个负数就sign乘以-1；有零直接返回0

```text
class Solution {
    public int arraySign(int[] nums) {
        
        int sign = 1;
        
        for (int num : nums) {
            if (num == 0) return 0;       
            if (num < 0) sign = sign * (-1);
        }
        
        return sign;
    }
}


```

两种方法时间均为O\(n\)；空间为 O\(1\)



注意要点：

返回时判断奇偶，可直接一行代码`return count % 2 == 0 ? 1 : -1;`





