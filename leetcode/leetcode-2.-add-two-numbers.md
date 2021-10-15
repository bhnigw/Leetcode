---
description: Linked List
---

# \[Leetcode]2. Add Two Numbers

原题地址：[https://leetcode.com/problems/add-two-numbers/](https://leetcode.com/problems/add-two-numbers/) 关键词：Linked List

题意：给两个**非空**的链表，表示两个**非负的整数**。它们每位数字都是按照**逆序**的方式存储的，并且每个节点只能存储**一位**数字。将两个数相加，并以相同形式返回一个表示和的链表。除了数字 0 之外，这两个数都不会以 0 开头。

![](../.gitbook/assets/addtwonumber1.jpg)

Input: `l1 = [2,4,3], l2 = [5,6,4]`；\
Output: `[7,0,8]`；\
Explanation: 342 + 465 = 807



### 算法：

两个数加起来和为10以内的话很简单，难点是在于如果加起来大于10的话，就需要进一位。

比如下图的例子，第二位数4 + 6等于10，第二位填0，数字1要进到第三位去，第三位的算法就是3 + 4 +1 = 8，所以第三位填8。怎样确定填到结果集的第二位数是几呢？用`"当前两个数之和" % 10`来计算。

所以，我们把要进一位的数字初始化为`extra = 0`，怎样确定这个进一位的数字是几呢？用`"当前两个数之和" / 10`来计算然后赋值给extra。

![](<../.gitbook/assets/Screen Shot 2021-08-05 at 12.01.23 AM (1).png>)

初始化ListNode dummy来记录结果，pre指向dummy，两个指针`pointer1`和`pointer2`分别指向l1和l2，每加一个数字往右边移动一位。l1和l2可能长短不一，如果短的走完了，就加0；

`pointer1`指到的数字为num1，`pointer2`指到的数字为num2，它们俩的和，和之前的进一位的数相加之和为num3，`num3 = extra + num1 + num2`；\
每次加完后，就要计算num3向下一个数进一位的数，也就是要更新extra的值：`extra = num3 / 10;`\
与此同时，计算填到结果集的数字：`num3 = num3 % 10;`\
然后把num3的值加入到pre后面的node：`pre.next = new ListNode(num);`

注意❗️❗️ 如果最后一个数字加完extra还不为0，说明最后两个数字之和大于10，说明还要进一位加在最后。

```
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode pre = dummy;
        ListNode p1 = l1;
        ListNode p2 = l2;
        int extra = 0;
        
        while (p1 != null || p2 != null) { // l1和l2可能长短不一
            int num1 = p1 == null ? 0 : p1.val; //如果短的走完了，就加0
            int num2 = p2 == null ? 0 : p2.val;
            int num3 = extra + num1 + num2;
            extra = num3 / 10;
            num3 %= 10;
            
            pre.next = new ListNode(num3);
                      
            if (p1 != null) { // 不能用p1.next != null，否则跳不出while loop
                p1 = p1.next;
            }
            if (p2 != null) {
                p2 = p2.next;
            }
            
            pre = pre.next;
        }
        
        
        if (extra != 0) { // 注意，如果最后一个数字加完extra还不为0，说明还要进一位
            pre.next = new ListNode(extra);
        }   
        
        return dummy.next; // 结果是从dummy.next开始记录的
    }
}
```

Time: `O(max(m,n))`；m和n分别为l1和l2的长度\
Space: `O(max(m,n))`；空间为新的list的长度，最长为`max(m, n) + 1`；



### 本题要记住的重点：

1. 怎样往ListNode后面加入新的node：`pre.next = new ListNode(num);`
2. 如果最后一个数字加完extra还不为0，说明最后两个数字之和大于10，说明还要进一位加在最后。







