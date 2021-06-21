---
description: '数学, StringBuilder, char, String'
---

# \[Leetcode\]171. Excel Sheet Column Number

原题地址：[https://leetcode.com/problems/excel-sheet-column-number/](https://leetcode.com/problems/excel-sheet-column-number/) 关键词：StringBuilder, char 

题意：letter to number；英文字母有26个，可以理解为把一个26进制的数转化为十进制的数；  
A -&gt; 1   
B -&gt; 2   
C -&gt; 3   
...   
Z -&gt; 26   
AA -&gt; 27   
AB -&gt; 28   
...

算法：把input string转化为char的array，然后**从右往左**\(相当于从26进制的个位数开始\)，char\[末尾\]算是个位数，然后加上char\[倒数第二\]乘以26\(相当于十位数\)，然后加上char\[倒数第三\]乘以26×26，然后加上char\[倒数第四\]乘以26×26×26，以此类推....

```text
class Solution {
    public int titleToNumber(String s) {
        int res = 0;
        
        char[] letter = s.toCharArray();
        int mult = 1;
        
        for (int i = letter.length - 1; i >= 0; i--) {
            
            res = (letter[i] - 'A' + 1) * mult + res;
            mult = mult * 26;
        }
        
        return res;
    }
}
```

Time: O\(n\)  
Space: O\(1\)

**注意**：  
1. 从右往左第一个字母，由于是个位数，就是字母本身所代表的数，不需要乘以26，所以第一个乘以的mult数必须是1，下一位数才开始乘以26；  
2. 代码第十行必须要加1，因为`letter[i] - 'A'`代表的只是该字母的index，而我们需要的是该字母在字母表中是第几个。比如输入letter是'A'，减去后是0，乘以mult后还是0，就不对；所以要加上1才能代表该字母的位置数。





Follow up：如何数字转化成字母？**number to letter**  
26 -&gt; Z  
28 -&gt; AB  
...

算法：用while loop处理余数；用`num % 26`得到一个小于26的余数remainder，这个余数就代表该字母在字母表中是第几个位置；这个余数减1就是该字母的index，然后`(char)(remainder - 1 + 'A')`就得出该字母，然后append到结果集中（它就代表了这个26进制数的个位数）。然后用把num值变为`num / 26`，此时用它除以26所得余数就是这个26进制数的十位数，以此类推。  
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

