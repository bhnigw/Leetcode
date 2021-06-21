---
description: Hash Set
---

# \[Leetcode\]187. Repeated DNA Sequences

原题地址：[https://leetcode.com/problems/repeated-dna-sequences/](https://leetcode.com/problems/repeated-dna-sequences/) 关键词：HashSet

题意：给一个DNA序列（一个string），目标子串的长度为 10，且在 DNA 字符串 s 中出现次数超过一次。



初步思路：跟

```text
class Solution {
    public List<String> findRepeatedDnaSequences(String s) { 
        List<String> res = new ArrayList<String>();
        if (s.length() < 10) return res;
        
        Set<String> set = new HashSet<String>();
     
        
        for (int i = 0; i + 10 <= s.length(); i++) {
            if (set.contains(s.substring(i, i + 10)) && !res.contains(s.substring(i, i + 10))) {
                res.add(s.substring(i, i + 10));
            } else {
                set.add(s.substring(i, i + 10));
            }
        }
        
        return res;
    }
}
```



```text
class Solution {
    public List<String> findRepeatedDnaSequences(String s) { 
        
        Set<String> seen = new HashSet<String>();
        Set<String> res = new HashSet<String>();
        
        for (int i = 0; i + 10 <= s.length(); i++) {
            if (seen.contains(s.substring(i, i + 10))) { //如果重复
                res.add(s.substring(i, i + 10));         //加到res的set里
            } else {
                seen.add(s.substring(i, i + 10));        //不重复就加到seen的set里
            }
        }
        
        return new ArrayList<String>(res);
    }
}
```

Time: O\(n\)  
Space: O\(n\)







