# \[Leetcode\]186. Reverse Words in a String II

原题地址：[https://leetcode.com/problems/reverse-words-in-a-string-ii/](https://leetcode.com/problems/reverse-words-in-a-string-ii/)

题意：给一个character array，保持单词本身的情况下，reverse整个句子顺序；input的单词间只有一个空格；  
例如：Input: `s = ['t','h','e',' ','s','k','y',' ','i','s',' ','b','l','u','e']`  
         Output: `s = ['b','l','u','e',' ','i','s',' ','s','k','y',' ','t','h','e']`

算法：先reverse整个char array，再分别reverse每一个单词即可；

重点是怎样分别reverse每一个单词：  
既然是char array，用while遍历，遇到空格则跳过，遇到单词，则**确定每个单词起始点、终点的index**，然后调用reverse的方法翻转这个单词即可；

```text
class Solution {
    public void reverseWords(char[] s) {
        if (s == null || s.length <= 1) return;
        
        int length = s.length;
        
        // 1. reverse whole char array
        reverse(s, 0, length - 1); 
        
        // 2. reverse each word 这一步可以写在内部也可以像reverse一样单独写在外面
        int start = 0;
        int end = 0;
        while (start < length && end < length) {
            while (end < length && s[end] != ' ') {
                end++;
            }
            reverse(s, start, end - 1);
            
            if (end < length && s[end] == ' ') {
                end++;
                start = end;
            }
        }
    }
    
    public void reverse(char[] s, int left, int right) {
        while (left < right) {
            char temp = s[left];
            s[left] = s[right];
            s[right] = temp;
            left++;
            right--;
        }
    }
}
```



Time：O\(N\)  
Space：O\(1\)

