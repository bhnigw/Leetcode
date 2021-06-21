# Valid Anagram

原题地址：[https://leetcode.com/problems/valid-anagram/](https://leetcode.com/problems/valid-anagram/)

Anagram定义：两个string，由**相同字母组成，但字母顺序被打乱**。An anagram is a word formed by rearranging the letters.

**事先要确认**：  
1. 是否都是小写字母lowercase / 是否是case sensitive？  
2. 是否有空格blankspace



方法一：sort两个string，看是否相等；

```text
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false; //string的长度不同，直接false         
    
        char[] str1 = s.toCharArray(); //转换成char数组
        char[] str2 = t.toCharArray();
    
        Arrays.sort(str1);  
        Arrays.sort(str2);
        
        return Arrays.equals(str1, str2); 
    }
}
```

Time: O\(nlogn\);      
Space: O\(1\) 

注意:  
1. 判断两个数组是否相等要用`Arrays.equals(nums1, nums2);`  
2. string要先toCharArray\(\)才能sort



方法二：记录字母出现次数\(最优\)；  
因为全是英文小写字母，所以new一个长为26的数组：`int[] count = new int[26];`在str1出现一次加一，在str2出现一次减一，最后数组应该都为0，否则是不是anagram。

```text
class Solution {
    public boolean isAnagram(String s, String t) {
        if (s.length() != t.length()) return false;
    
        int[] count = new int[26];
    
        for (int i = 0; i < s.length(); i++) {        
            count[s.charAt(i) - 'a']++;       
            count[t.charAt(i) - 'a']--;
        }
    
        for (int num : count) {
            if (num != 0) return false;
        }
    
        return true;
    }
}
```

Time: O\(n\)  
Space: O\(1\)



