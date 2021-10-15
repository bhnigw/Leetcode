# \[Leetcode]214. Shortest Palindrome

原题地址：[https://leetcode.com/problems/shortest-palindrome/](https://leetcode.com/problems/shortest-palindrome/) 关键词：Palindrome

题意：给一个string，你可以通过在string前面添加字符，将其转换为一个Palindrome的string。找到并返回可以用这种方式转换的**最短**Palindrome。

例：\
Input: `s = "acecaaa"`\
Output: `"aaacecaaa"`



### 算法：

核心思想：从最右边right开始，找到第一个到index 0为Palindrome的地方，记下这个index，然后把这个index后面部分翻转后加到最前面。

![](../.gitbook/assets/IMG\_6486.jpg)

```
class Solution {
    public String shortestPalindrome(String s) {
        if (s.length() <= 1) return s;
        
        int left = 0, right = s.length() - 1;
        
        while (left < right) {
            if (isPalindrome(s.substring(0, right + 1), 0, right)) {
                break;
            } else {
                right--;
            }
        }
        
        if (right == s.length() - 1) {
            return s;
        } else {
            StringBuilder sb = new StringBuilder(s.substring(right + 1, s.length())); // 注意是right + 1
            return sb.reverse().append(s).toString();
        }
    }
    
    private boolean isPalindrome(String s, int left, int right) {
        
        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) return false;
            
            left++;
            right--;
        }
        
        return true;
    }
}
```

Time: O(n ^ 2)

Space: O(n)





