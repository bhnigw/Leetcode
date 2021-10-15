---
description: Linked List
---

# \[Leetcode]21. Merge Two Sorted Lists

原题地址：[https://leetcode.com/problems/merge-two-sorted-lists/](https://leetcode.com/problems/merge-two-sorted-lists/) 关键词：Linked List

题意：合并2个升序链表。\
将两个升序的LinkedList，合并为一个新的升序LinkedList并返回。

例：\
Input: `l1 = [1,2,4], l2 = [1,3,4] `\
Output: `[1,1,2,3,4,4]`



### 算法：

**核心思想：**两两比较，连接最小的。

用`cur`指针来扫所有的，`l1`和`l2`当作双指针来扫两个链表；两两比较，把更小的连接到`cur.next`，直到`l1`和`l2`指针其中一个指向null；

![](../.gitbook/assets/IMG\_6460.jpg)



![](../.gitbook/assets/IMG\_6461.jpg)



当有`l1`, `l2`其中一个指针指向null时，把剩余的链表直接连到`cur.next`（因为剩余部分是sorted）：

![](../.gitbook/assets/IMG\_6463.jpg)



最终结果：返回`dummy.next`即可

![](../.gitbook/assets/IMG\_6465.jpg)

###  要注意的地方：

while loop只能处理等长的部分，其中一个链表到达null后就停止了loop。所以当有`l1`, `l2`其中一个指针指向null时，把剩余的链表直接连到`cur.next`中，因为剩余部分是sorted。（代码第19～24行）

```
class Solution {
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(-1);
        ListNode cur = dummy;
        
        while (l1 != null && l2 != null) { // 处理等长的部分
            if (l1.val < l2.val) {
                cur.next = l1;
                l1 = l1.next;  // 这一步可能l1已经到了终点null
                cur = cur.next;               
            } else {
                cur.next = l2;
                l2 = l2.next;
                cur = cur.next;               
            }
        }
        
        
        if (l1 != null) {  // 如果l1和l2不等长，那么下面是处理后面不等长的部分 
            cur.next = l1;
        }
        if (l2 != null) { 
            cur.next = l2;
        }
        
        return dummy.next;
    }
}
```

Time: `O(n + m)`；n是l1的节点总数，m是l2的节点总数；\
Space: `O(n + m)`；最终list的size





#### Follow up:

{% content-ref url="leetcode-23.-merge-k-sorted-lists.md" %}
[leetcode-23.-merge-k-sorted-lists.md](leetcode-23.-merge-k-sorted-lists.md)
{% endcontent-ref %}



