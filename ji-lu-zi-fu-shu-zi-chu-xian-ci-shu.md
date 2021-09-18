# 检查重复、统计字符或数字出现次数

## 检查重复：

检查重复，其本质也是统计出现次数。“不允许重复“，换句话说，就是出现的次数不能超过1次；

❗️ 一看到 **“重复“** / **“duplicate“** 这两个字，就应该立马联想到HashSet！

对于不允许重复/只允许出现一次这类题目，用HashSet是最方便的；



例：

```text
    Set<Character> set = new HashSet<>();

		for (int i : nums) {
			if (!set.add(i)) {
				return false;
			}
		}
```

解释：HashSet里的`add()`方法本身就可以判断set里是否已经含有该元素，且会返回一个boolean值，如果`add()`返回false，说明有重复；



## 统计数字或字母的出现次数

### 方法一：用数组来记录出现次数

#### 情况1：统计数字（适用于题目的input只含个位数0～9）

方法：使用长度为10的`nums[]`数组，数字出现一次就在对应的index加一：`nums[ch - '0']++;`

```text
		char[] Array = { '3', '5', '3', '1' };
		int[] nums = new int[10];

		for (char ch : Array) {
			nums[ch - '0']++;
		}
```

`nums[]`的长度为10，对应数字0～9，`'0'`的index是0，`'1'`的index是1，是一一对应的；

此时nums等于`{ 0, 1, 0, 2, 0, 1, 0, 0, 0, 0 }`

延伸拓展：如果题目的input数字只在3～8范围，那么`nums[]`长度应设为6，操作应为`nums[ch - '3']`；  
因为数字字符`'3'`对应的index是0；

#### 情况2：统计英文字母

如果只有大写字母，或只有小写字母

方法：使用长度为26的`letters[]`数组，字母出现一次就在对应的index加一：  
`letters[ch - '0']++;`

#### 情况3：同时统计字母和数字

方法：使用长度为128的`ascii[]`数组，字符出现一次就在对应的index加一：`ascii[ch]++;`

**char字符作为index直接放进数组**，不用担心任何指数问题，不用减去任何东西，很方便，所以count字符的问题都推荐此方法，很universal；

```text
		char[] Array = { '3', '5', '3', '3', 'J', 'a', 'k', 'e', };
		int[] ascii = new int[128];

		for (char ch : Array) {
			ascii[ch]++;             //char字符作为index直接放进数组
		}
```



### 方法二：使用HashMap，其中key作为被统计的元素，value为出现次数；

```text
public static void main(String[] args) {

		int[] nums = { 3, 5, 3, 3, 7, 8, 9, 9, 2 };
		Map<Integer, Integer> map = new HashMap<>();

		for (int i : nums) {
			if (!map.containsKey(i)) {
				map.put(i, 1);
			} else {
				int count = map.get(i);
				map.put(i, ++count);   //注意这里如果++写在了后面就有错
			}
		}

		System.out.println(map);

}
```

map输出为：`{2=1, 3=3, 5=1, 7=1, 8=1, 9=2}`

★更简便的写法：

```text
		Map<Integer, Integer> map = new HashMap<>();

		for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1); // 计算频率
        }
```



#### 要记住的重点：

1. map.get\(i\)后面不能直接++；
2. `++count`写在前面意思是先进行加1运算，再操作，如果是`count++`意思就是先操作了再加1，是不对的；

