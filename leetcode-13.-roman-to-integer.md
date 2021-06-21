---
description: HashMap，罗马数字
---

# \[Leetcode\]13. Roman to Integer

原题地址：[https://leetcode.com/problems/roman-to-integer/](https://leetcode.com/problems/roman-to-integer/) 关键词：HashMap，罗马数字

题意：将罗马数字转换为阿拉伯数字。

例：  
`Input: s = "III"；  
Output: 3`

`Input: s = "IV"；  
Output: 4`



古罗马数字基本符号：

![](.gitbook/assets/screen-shot-2021-06-14-at-11.49.28-pm.png)

**记数方法：**  
1. 相同的字母连写，表示的数是：这些字母连续相加得到的数，如：`III = 3；`  
2. 左大右小，表示的数是：这些字母直接相加得到的数， 如：`VIII = 8，XII = 12；`   
3. 左小右大，表示的数是：右边大的数减去左边小的数，如：`IV = 4，IX = 9；`



由上面记数方法可知，罗马数字转换阿拉伯数字会出现两种情况：

**第一种情况**：记数方法1、2，这种情况很好处理，直接把所有字母代表的数字相加即可；

**第二种情况**：记数方法3，这种情况较为特殊，需要用右边大的数减去左边小的数；如下：  
****Symbol：  `IV  IX  XL   XC   CD   CM`  
Value：     `4   9   40   90   400  900` 

\*\*\*\*

**算法：**

1.先用HashMap存储罗马数字的符号和其代表的数字；HashMap的key是符号，value是对应的数字；

2.初始化一个res值，把input string的第一个字母代表的值赋值给它`res = map.get(str.charAt(0));`

3.初始化一个prev值，用于比较两个字母时候，用当前字母和prev来比较；`prev = s.charAt(i);`

4.用for loop，从i = 1开始，**从左至右**遍历input string，依次相加的同时，比较当前字母和prev字母，如果当前字母的值比prev的大，则继续；`res = map.get(s.charAt(i)) + res;`

5.继续依次相加的同时，比较当前字母和prev字母，如果当前字母的值比prev的小，那么说明遇到了上面情况二，需要用右边的字母减去左边的，由于res值是从左至右依次相加的，所以prev的值需要减去两次；`res = map.get(s.charAt(i)) - 2 * map.get(prev) + res;`

6.记得每一轮for loop都要更新prev的值，进入下一轮之前，把当前值赋给它；

```text
class Solution {
    public int romanToInt(String s) {
        if (s == null || s.length() == 0) return 0;
        
        HashMap<Character, Integer> map = new HashMap<>();
        map.put('I', 1);
        map.put('V', 5);
        map.put('X', 10);
        map.put('L', 50);
        map.put('C', 100);
        map.put('D', 500);
        map.put('M', 1000);

        int res = 0;
        char prev = s.charAt(0);
        res = map.get(prev);
            
        for (int i = 1; i < s.length(); i++) {
            if (map.get(s.charAt(i)) > map.get(prev)) {
                res = map.get(s.charAt(i)) - 2 * map.get(prev) + res; //减两次
            } else {
                res = map.get(s.charAt(i)) + res;
            }
            
            prev = s.charAt(i);
        }
                              
        
        return res;
    }
}
```

Time & Space：  
如果给定的input string有长度限制，那Time和Space都是O\(1\)；  
如果input string长度不限制，那Time和Space都是O\(n\)；





### 本题要记住的地方：

1. 用HashMap记录对应关系；
2. for loop，从i = 1开始（初始化一个prev值charAt\(0\)）；
3. 特殊情况把prev值减两次；



