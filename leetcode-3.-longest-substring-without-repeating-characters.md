---
description: 'Slide window, Hash set'
---

# \[Leetcode\]3. Longest Substring Without Repeating Characters

原题地址：[https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)  
关键词：Slide window, Hash set

题意：给一个string，找出其中不含有重复字符的最长substring的长度。



方法一：Brute force；

方法二：Slide window；  
1. 跟duplicate有关，那么就用HashSet，然后初始一个left慢指针和一个right快指针。  
2. 使用right指针看新字母是否在set，如果没有就将它添加到set，然后更新最大长度，然后right++；  
3. 如果新字母已经存在set里了，说明它与当前的substring开头的第一个字母重复，那么我们就用`set.remove()`删去第一个字母`str.charAt(left)`，然后left++，使新的substring没有重复。

```text
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) return 0;
        
        int res = 0;
        
        Set<Character> set = new HashSet<Character>();
        int left = 0, right = 0;
        
        while (right < s.length()) {
            if (!set.contains(s.charAt(right))) { //如果新的字母set里没有
                set.add(s.charAt(right));         //那就加入set
                res = Math.max(res, set.size());  //更新最大长度
                right++;                          //right右移
            } else {                              //如果新字母set已有
                set.remove(s.charAt(left));       //把left重复的字母去掉
                left++;                           //left右移
            }         
        }
        
        return res;
    }
}
```

Time: O\(n\)  
Space: O\(n\)； 取决于set的size，而set的size取决于string的长度，所以是n





类似题目：187. Repeated DNA Sequences









