---
description: '数学, char, String'
---

# \[Leetcode\]171. Excel Sheet Column Number

原题地址：[https://leetcode.com/problems/excel-sheet-column-number/](https://leetcode.com/problems/excel-sheet-column-number/)  

题意：字母转化为数字；规则如下：  
A -&gt; 1   
B -&gt; 2   
C -&gt; 3   
...   
Z -&gt; 26   
AA -&gt; 27   
AB -&gt; 28   
...

例1：  
`Input: columnTitle = "AB"； Output: 28`  
例2：  
`Input: columnTitle = "ZY"； Output: 701`



### 算法：

可以理解为把一个二十六进制（base of 26）的数转化为十进制（decimal）的数；

![](../.gitbook/assets/img_6402.jpg)

所以，从右向左，遍历input string，每一位的基数乘以26的次方，幂数从0开始依次加一，最后加起来即可

我们要做的就是确定每一位的基数即可。怎么确定每一位字母代表的数字呢？  
可以使用ASCII码里指数的位置差：`ch - 'A' + 1` （[详情点击查看ASCII讲解](https://bhnigw.gitbook.io/-1/shu-ju-jie-gou-string/ascii-ma)）

怎样运算次方呢？  
用`Math.pow(x, y)`，x代表底数，y代表次幂，也就是相当于`x ^ y`

```text
class Solution {
    public int titleToNumber(String columnTitle) {
        if (columnTitle == null || columnTitle.isEmpty()) return 0;
        
        int res = 0;
        int pow = 0;
        
        for (int i = columnTitle.length() - 1; i >= 0; i--) { // 注意是i>=0
            char ch = columnTitle.charAt(i);
            res += (ch - 'A' + 1) * Math.pow(26, pow);
            pow++;
        }        
        
        return res;
    }
}
```

Time: O\(n\)  
Space: O\(1\)

**注意**：  
1. 代码第10行必须要加1，因为`ch - 'A'`代表的只是该字母的index，而我们需要的是该字母在字母表中是第几个。比如输入letter是'A'，减去后是0，后面乘起来依然是0就不对了；所以要加上1才能代表该字母的位置数。  
2. 怎样计算次幂；  
3. 如果for循环是从后往前，那么`for (int i = nums.length - 1; i >= 0; i--)` 一定是`i >= 0`



英语词汇：

`exponential` adj. 指数的； exponential function 指数函数

`exponent` n. 指数，幂



### ❗️Follow up：如何数字转化成字母？（number to letter）

26 -&gt; Z  
28 -&gt; AB  
...

#### 算法：

用while loop处理余数；用`num % 26`得到一个小于26的余数remainder，这个余数就代表该字母在字母表中是第几个位置；这个余数减1就是该字母的index，然后`(char)(remainder - 1 + 'A')`就得出该字母，然后append到结果集中（它就代表了这个26进制数的个位数）。然后用把num值变为`num / 26`，此时用它除以26所得余数就是这个26进制数的十位数，以此类推。  
要额外考虑余数remainder是0的情况，因为如果余数是0，则表明字母是'Z'，但是`(char)(remainder - 1 + 'A')` 就会得出-1，不能得出'Z'

```text
	public String NumberToLetter(int num) {
		StringBuilder sb = new StringBuilder();
		
		while (num > 0) {
			int remainder = num % 26;
			if (remainder == 0) { //如果余数是0
				sb.append("Z");
				num = num - 1;
			} else {             //余数非0
				sb.append((char)(remainder - 1 + 'A'));
			}
			num = num / 26;
		}
		
		return sb.reverse().toString();
	}
```

Time: O\(1\)  
Space: O\(1\)

**注意**：  
1. 因为string是从个位开始append，所以最后要记得reverse然后toString\(\)；  
2. 第8行为什么要减1？因为如果输入是26，在不减一的情况下运行到12行，num就会变成1然后继续while循环，得到错误的'AZ'答案，所以如果余数是0则需要num减一，才能保证12行num是0

