---
description: Two pointer，Palindrome
---

# 判断Palindrome

### 定义：

**Palindrome**：A word or phrase that reads the same backward as forward.\
回文，即一个string正着看和倒着看，它的字母顺序都是一样的。



若题目没有额外的要求，就用two poniter方法，比较首位两个字符是否相同即可：

```
public boolean isPalindromic(String str) {
		int i = 0;
		int j = str.length() - 1;

		while (i < j) {
			if (str.charAt(i) != str.charAt(j)) return false;

			i++;
			j--;
		}

		return true;
}
```





## 例题：[125. Valid Palindrome](https://leetcode.com/problems/valid-palindrome/)

题意：给个string，可能含有空格或者特殊符号，需要判断出现的**字母和数字**是不是Palindrome，如果是就返回true；

例：\
Input: `s = "A man, a plan, a canal: Panama" `\
Output: `true` \
Explanation: "amanaplanacanalpanama" is a palindrome.



### 方法一：Compare with Reverse；

把字母append到StringBuilder里面形成str1，然后反转顺序形成str2，如果str1和str2相等那就是palindrome

```
class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder builder = new StringBuilder();

        for (char ch : s.toCharArray()) {
            if (Character.isLetterOrDigit(ch)) {
                builder.append(Character.toLowerCase(ch));
            }
        }

        String str1 = builder.toString();
        String str2 = builder.reverse().toString();

        return str1.equals(str2);
    }
}
```

Time: O(n)\
Space: O(n)；str的长度是n，需要n空间来build它



### 方法二：Two pointer(最优)；

跳过所有的空格和标点，然后首尾比较。

```
class Solution {
    public boolean isPalindrome(String s) {
        if (s.isEmpty()) { //为空则为true
        	return true;
        }
        
        int left = 0, right = s.length() - 1;
        char charLeft, charRight;   //注意初始化字符串的格式
        
        while(left < right) { //two pointer方法
        	charLeft = s.charAt(left);
        	charRight = s.charAt(right);
        	if (!Character.isLetterOrDigit(charLeft)) { //跳过空格和标点，只看字母和数字的情况
        		left++;
        	} else if(!Character.isLetterOrDigit(charRight)) { //跳过空格和标点，只看字母和数字的情况
        		right--;
        	} else {
        		if (Character.toLowerCase(charLeft) != Character.toLowerCase(charRight)){//首尾不同则是false
        			return false;
        		}
        		left++;
        		right--;
        	}
        }
        
        return true;
    }
}
```

Time: O(n)\
Space: O(1)

注意：\
1\. **`Character.isLetterOrDigit(char ch)` 用于判断character是字母还是数（letter or digit）**\
2\. `Character.isLetter(char ch)`返回true那这个Character就是字母 \
3\. `Character.isDigit(char ch)`返回true那这个Character就是数字



关于Character的复习：



