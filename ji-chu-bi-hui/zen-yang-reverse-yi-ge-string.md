# 怎样reverse一个String

方法一：使用StringBuilder里的build in function

```text
public String ReverseString(String str) {
		StringBuilder sb = new StringBuilder(str);
		return sb.reverse().toString();
	}
```



方法二★：two pointer

1. 把str变为char array；
2. 设置left pointer为0，right pointer为str长度减一；
3. 对left和right进行交换swap，需要借助中间字符temp，然后left++，right--；

```text
public String ReverseString(String str) {
		char arr[] = str.toCharArray();
		int left = 0;
		int right = str.length() - 1;
		
		while (left < right) {
			char temp = arr[left];
			arr[left] = arr[right];
			arr[right] = temp;
			left++;
			right--;
		}
		
		return new String(arr); 
	}
```

注意：  
1. while那里是小于  
2. 怎样把char array转化为string  
3. 最后return也可以用 String.valueOf\(arr\);

复习string和char array的转换：[https://bhnigw.gitbook.io/-1/](https://bhnigw.gitbook.io/-1/)

