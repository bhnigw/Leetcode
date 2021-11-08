# \[Leetcode]28. Implement strStr()

原题地址：[https://leetcode.com/problems/implement-strstr/](https://leetcode.com/problems/implement-strstr/)

题意：给两个字符串`haystack`和`needle`，要求在`haystack`中找出`needle`出现的第一个位置（下标从0开始）。如果不存在，则返回 -1。如果`needle`为null，返回 0；

例：\
Input: `haystack = "hello", needle = "ll"`\
Output: 2



### 方法1：

**核心思想：**遍历`haystack`里的字母，遇到与`needle`第一个字母相同的地方时停下，从这里往后面看，看后面的几个字母是否和`needle`字母完全相同，若相同则返回停下时的index。

```
class Solution {
    public int strStr(String haystack, String needle) {       
        int res = -1;
        
        if (haystack == null || needle == null || haystack.length() < needle.length()) return res;
        if (needle.length() == 0 || haystack.equals(needle)) return 0;
        
        for (int i = 0; i < haystack.length(); i++) {
            if (haystack.charAt(i) == needle.charAt(0)) { // 遇到相同字母
                int index = 0;
                for (int j = i; j < haystack.length() && index < needle.length(); j++) {
                    if (haystack.charAt(j) != needle.charAt(index)) break; //注意这里已经判断了不相等
                    
                    if (index == needle.length() - 1) { // Index到达末尾且char相等
                        res = i;
                        return res;
                    }
                    
                    index++;
                }
            }
        }
        
        return res;
    }
}
```

Time：`O(n × m)`；其中n是字符串`haystack`的长度，m是字符串`needle`的长度。最坏情况下我们需要将`needle`与`haystack`的所有长度为m的substring均匹配一次。

Space：`O(1)`；

在第8行中，如果在condition的判断里加上`haystack.length() - i >= needle.length();`的话，时间会更加优化，意思是如果haystack剩下的长度小于了needle的长度，那么就不用再判断了因为肯定装不下needle。



### 方法2：Build in method（一般不允许使用）

**核心思想：**遍历`haystack`里的字母，遇到与`needle`第一个字母相同的地方时停下，从这里往后面看，看后面substring是否和`needle`完全相同，若相同则返回停下时的index。

```
public class Solution {
    public int strStr(String haystack, String needle) {
        int l1 = haystack.length(), l2 = needle.length();
        if (l1 < l2) {
            return -1;
        } else if (l2 == 0) {
            return 0;
        }
        
        int threshold = l1 - l2;
        for (int i = 0; i <= threshold; ++i) {
            if (haystack.substring(i,i+l2).equals(needle)) {
                return i;
            }
        }
        
        return -1;
    }
}
```





