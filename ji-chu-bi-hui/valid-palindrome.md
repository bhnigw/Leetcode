---
description: Two pointer
---

# Valid Palindrome

原题地址：[https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

Palindrome定义：回文，即一个string正着看和倒着看，它的字母顺序都是一样的；A word or phrase that **reads the same backward as forward**.



方法一：Compare with Reverse；把字母append到StringBuilder里面形成str1，然后反转顺序形成str2，如果str1和str2相等那就是palindrome

```text
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

Time: O\(n\)  
Space: O\(n\)；str的长度是n，需要n空间来build它



方法二：Two pointer\(最优\)；跳过所有的空格和标点，然后首尾比较。

```text
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

Time: O\(n\)  
Space: O\(1\)

注意：  
1. **`Character.isLetterOrDigit(char ch)` 用于判断character是字母还是数（letter or digit）**  
2. `Character.isLetter(char ch)`返回true那这个Character就是字母   
3. `Character.isDigit(char ch)`返回true那这个Character就是数字



关于Character的复习：[https://app.gitbook.com/@bhnigw/s/-1/shu-ju-jie-gou-string](https://app.gitbook.com/@bhnigw/s/-1/shu-ju-jie-gou-string)













