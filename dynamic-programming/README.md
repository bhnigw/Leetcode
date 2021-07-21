---
description: Dynamic Programming，DP
---

# Dynamic Programming问题总结

**动态规划\(DP\)的基本思想：**若要解一个给定问题，我们需要解其不同部分，即「子问题」，再根据子问题的解以得出原问题的解。通常许多子问题非常相似，因此一旦某个子问题的解已经算出，则将其记忆化存储，下次需要同一个子问题解之时可以直接查表，从而减少计算量。



### DP与Recursion：

DP是「自底向上」，Recursion是「自顶向下」。

是什么意思？？以Fibonacci来举例解释：

「**自顶向下」**的意思是：从一个规模较大的原问题比如`fib(20)`，向下逐渐分解规模，直到`fib(1)`和`fib(2)`触底，然后逐层返回答案，这就叫「自顶向下」。

```text
public static int Fibonacci(int n) {
		if (n <= 1) {
			return n;
		}
		return Fibonacci(n - 1) + Fibonacci(n - 2);
	}
```



「**自底向上」**的意思是：从最底下，问题规模最小的`fib(1)`和`fib(2)`开始往上推，直到推到我们想要的答案`fib(20)`，这就是动态规划DP的思路。

```text
public int Fibonacci(int n) {
		int dp[] = new int[n + 1]; 

		dp[0] = 0; 
		dp[1] = 1;

		for (int i = 2; i <= n; i++) { 
			dp[i] = dp[i - 1] + dp[i - 2];
		}

		return dp[n];
	}
```

###  <a id="&#x72B6;&#x6001;&#x8F6C;&#x79FB;&#x65B9;&#x7A0B;"></a>

### 状态转移方程

{% hint style="warning" %}
状态转移方程就是用**数学形式**来描述问题结构，它是解决问题的核心。
{% endhint %}

只要动态规划问题最困难的就是写出状态转移方程，



### 经典例题：

[斐波那契数列 Fibonacci number](https://bhnigw.gitbook.io/leetcode/fei-bo-na-qi-shu-lie-fibonacci-number)

[70. 爬楼梯](https://bhnigw.gitbook.io/leetcode/leetcode-70.-climbing-stairs)

[518. Coin Change 2](https://bhnigw.gitbook.io/leetcode/leetcode-518.-coin-change-2)

[53. Maximum Subarray](https://bhnigw.gitbook.io/leetcode/leetcode-53.-maximum-subarray)





