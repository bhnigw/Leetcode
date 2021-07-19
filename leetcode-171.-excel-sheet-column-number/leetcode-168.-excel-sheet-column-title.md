# \[Leetcode\]168. Excel Sheet Column Title

原题地址：[https://leetcode.com/problems/excel-sheet-column-title/](https://leetcode.com/problems/excel-sheet-column-title/)

题意：数字转化为字母；规则如下：  
A -&gt; 1   
B -&gt; 2   
C -&gt; 3   
...   
Z -&gt; 26   
AA -&gt; 27   
AB -&gt; 28   
...

例1：  
`Input: columnNumber = 28； Output: "AB"`  
例2：  
`Input: columnNumber = 701； Output: "ZY"`



### 算法：

核心思想：  
对十进制\(decimal\)的数来说，number用求余符号`"%"`对10求余数，得到的余数就是最右边的**个位数**。然后用取整符号`"/"`除以10更新number，再继续用%10求余数就得到了十位数，然后不断重复此过程...

举例：`number = 123`：  
先把number用`"%"`对10求余：123 % 10 = 3，说明个位数就是3；  
然后number用`"/"`除以10，看能被整除几次：123 / 10 = 12，说明number能被10整除12次；\(number里有12个10\)

十位数应该是12，但因为是10进制，所以对12求余：12 % 10 = 2，所以十位数就是2；  
继续把number用`"/"`除以10得：12 / 10 = 1，意思是number能被100整除1次；  
所以百位数应该是1，但因为是10进制，所以对1求余：1 % 10 = 1，所以百位数就是1；

每求余一次`"%"`，就得出一位数字。

![](../.gitbook/assets/img_6403.jpg)



![](../.gitbook/assets/img_6405.jpg)

同理：  
对26进制\(base of 26\)的数来说，number用求余符号`"%"`对26求余数，得到的余数就是最右边的"**个"位数**。然后用取整符号`"/"`除以26更新number，再继续用%26求余数就得到了"十"位数，然后不断重复此过程...

举例：`number = 123`：  
先把number用`"%"`对26求余：123 % 26 = 19，说明"个"位数就是二十六进制中的19\(也就是字母S\)；  
然后number用`"/"`除以26，看能被整除几次：123 / 26 = 4，说明number能被26整除4次；\(number里有4个26\)

"十"位数应该是4，但因为是26进制，所以对4求余：4 % 26 = 4，所以"十"位数就是二十六进制中的4\(也就是字母D\)；  
继续把number用`"/"`除以26得：4 / 26 = 0，结束循环。

每求余一次`"%"`，就得出一位数字。

要注意的是：

```text
class Solution {
    public String convertToTitle(int columnNumber) {
        StringBuilder sb = new StringBuilder();
        
        while (columnNumber > 0) {
            columnNumber--;    //注意这里
            sb.append((char)(columnNumber % 26 + 'A'));
            columnNumber /= 26;
        }

        return sb.reverse().toString();
    }
}
```





### 需要记住的重点：

1. 数字一定要先减1❗️
2. 因为是从个位开始append，所以最后转化为string前要先reverse；







