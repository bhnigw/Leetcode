---
description: Doubly LinkedList，双向链表，HashMap
---

# \[Leetcode\]★146. LRU Cache

原题地址：[https://leetcode.com/problems/lru-cache/](https://leetcode.com/problems/lru-cache/) 关键词：Doubly LinkedList，双向链表

题意：设计和实现一个“最近最少使用“的缓存机制Least Recently Used cache \(LRU\)，  
实现下面三个方法：  
●`LRUCache(int capacity)`：初始化正整数capacity，作为LRU的缓存容量；  
●`int get(int key)`：如果关键字key存在于LRU Cache中，则返回关键字的值；不存在就返回 -1 。   
●`void put(int key, int value)`：如果key已经存在，则变更其value值；如果key不存在，则插入该组「key-value pair」。当LRU Cache容量达到上限时，它应该在写入新数据之前，删除最久未使用的数据值，从而为新的数据值留出空间。

Follow up：是否可以在 O\(1\) 时间复杂度内完成这两种操作？













可以理解为map就是用来存数据的缓存cache

