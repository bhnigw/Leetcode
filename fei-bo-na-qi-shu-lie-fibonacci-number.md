---
description: Fibonacci
---

# 斐波那契数列 Fibonacci number

斐波那契数列指的这样一个数列：0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377 ,610, 987……

**从第3项开始，每一项都等于前两项之和。**特別指出：0不是第一項，而是第零項。

用数学表示就是：

![](.gitbook/assets/screen-shot-2021-07-20-at-12.30.22-am.png)

怎样用程序求第n个Fibonacci数字呢？



### 方法一：Recursion（不推荐）

优点：好理解；缺点：时间复杂度太高；

```text
	public static int Fibonacci(int n) {
		if (n <= 1) {
			return n;
		}
		
		return Fibonacci(n - 1) + Fibonacci(n - 2);
	}
```

Time: `O(2 ^ n)`; 解释：T\(n\) = T\(n - 1\) + T\(n - 2\); 比如下图，当n=5时，调用了16次fib\(\)方法，所以是指数复杂度（**exponential**）；

![](.gitbook/assets/img_6420.jpg)

Space: O\(n\); 解释：按深度算，每return一次创建一个空间。



### 方法二：Dynamic Programming

```text
	public int Fibonacci(int n) {
		int dp[] = new int[n + 2]; // 需要1个额外的空间来处理n = 0的情况

		dp[0] = 0;
		dp[1] = 1;

		for (int i = 2; i <= n; i++) { // 初始值是2
			dp[i] = dp[i - 1] + dp[i - 2];
		}

		return dp[n];
	}
```

### 方法三：Dynamic Programming 优化 （optimal）








