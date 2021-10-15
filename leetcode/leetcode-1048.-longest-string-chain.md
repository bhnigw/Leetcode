---
description: Dynamic Programming，DP
---

# \[Leetcode]1048. Longest String Chain

原图地址：[https://leetcode.com/problems/longest-string-chain/](https://leetcode.com/problems/longest-string-chain/) 关键词：HashMap，Dynamic Programming，DP

题意：如果我们可以在 word1 的任何地方添加一个字母使其变成 word2，那么我们认为 word1 是 word2 的前身**predecessor**。例如，"abc" 是 "abac" 的前身。\
词链是单词 \[word\_1, word\_2, ..., word_k] 组成的序列，k >= 1，其中 word\_1 是 word\_2 的前身，word\_2 是 word\_3 的前身，依此类推。从给定单词列表 words 中选择单词组成词链，返回词链的最长可能长度。

例：\
Input: `words = ["a", "b", "ba", "bca", "bda", "bdca"]`\
Output: 4\
Explanation: One of the longest word chains is `["a", "ba", "bda", "bdca"]`.



### 算法：

使用HashMap，key是单词，value是当前单词可以组成词链的最大长度。

先根据words数组里每个单词的长度，把单词从小到大排序。

遍历单词，把当前单词`curWord`里面每个字母挨个删去一遍，在删除的过程中会形成一个新单词`prev`，如果这个新单词在map中之前已经存在，就把这个`prev`单词可以组成词链的最大长度拿出来，+ 1，赋值给map里curWord对应的value。

最后对比得出最大的res即可。

```
class Solution {
    public int longestStrChain(String[] words) {
        if (words.length < 1) return 0;
        
        int res = 1; // 注意初始值是1
        Arrays.sort(words, (str1, str2) -> str1.length() - str2.length()); //根据words数组里每个单词的长度，把单词从小到大排序
        
        Map<String, Integer> map = new HashMap<>();
        
        for (String str : words) { // 先把所有单词放进map，初始value都是1
            map.put(str, 1);
        }
        
        for (String str : words) {  
            for (int i = 0; i < str.length(); i++) {
                StringBuilder curWord = new StringBuilder(str);
                StringBuilder prev = curWord.deleteCharAt(i);
                if (map.containsKey(prev.toString())) {
                    map.put(str, map.get(prev.toString()) + 1);  // 注意前面的key，和后面get的是什么
                    res = Math.max(res, map.get(str));
                }
            }
        }
        
        return res;
    }
}
```

Time: `O(NlogN + (N * L))`；前面部分sort的时间是`O(NlogN)`，后面部分遍历单词的时间是`O(N * L)`

Space: `O(N)`；map的size





