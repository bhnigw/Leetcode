---
description: StringBuilder
---

# \[Leetcode\]6. ZigZag Conversion

原题地址：[https://leetcode.com/problems/zigzag-conversion/](https://leetcode.com/problems/zigzag-conversion/) 关键词：StringBuilder

题意：将一个字符串`s`根据给定的行数`numRows`，进行ZigZag排列后，按照行数，重建string并返回。

例如：  
Input: s = `"PAYPALISHIRING"`, `numRows = 4`   
Output: `"PINALSIGYAHRPI"`   
解释:   
`P      I      N   
A    L S    I G   
Y  A   H  R   
P      I`



### 算法：

![](../.gitbook/assets/screen-shot-2021-08-08-at-4.55.27-pm.png)



```text
class Solution {
    public String convert(String s, int numRows) {
        // 题目规定了s的长度大于1，所以不用null check
        
        StringBuilder[] sb = new StringBuilder[numRows];
        StringBuilder res = new StringBuilder();
        int index = 0;
        
        for (int i = 0; i < numRows; i++) { //要初始化，否则nullPointerException
            sb[i] = new StringBuilder();
        }
        
        
        while (index < s.length()) {
            for (int i = 0; i < numRows && index < s.length(); i++) {
                sb[i].append(s.charAt(index));
                index++;
            }
            for (int j = numRows - 2; j > 0 && index < s.length(); j--) { //注意j初始值
                sb[j].append(s.charAt(index));
                index++;
            }
        }
        
        
        for (int i = 0; i < numRows; i++) {
            res.append(sb[i]);
        }
        
        return res.toString();
    }
}
```























