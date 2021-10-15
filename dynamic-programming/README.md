---
description: Dynamic Programming，DP
---

# Dynamic Programming问题总结

**动态规划(DP)的基本思想：**若要解一个给定问题，我们需要解其不同部分，即「子问题」，再根据子问题的解以得出原问题的解。通常许多子问题非常相似，因此一旦某个子问题的解已经算出，则将其记忆化存储，下次需要同一个子问题解之时可以直接查表，从而减少计算量。



### DP与Recursion：

DP是「自底向上」，Recursion是「自顶向下」。

是什么意思？？以计算Fibonacci题来举例解释，如果使用Recursion：

![](<../.gitbook/assets/Screen Shot 2021-07-21 at 2.05.38 AM.png>)

「**自顶向下」**的意思是：从一个规模较大的原问题比如`fib(4)`，向下逐渐分解规模，直到`fib(1)`和`fib(2)`触底，然后逐层返回答案，这就叫自顶向下（**Top-down**）。

```
public static int Fibonacci(int n) {
		if (n <= 1) {
			return n;
		}
		return Fibonacci(n - 1) + Fibonacci(n - 2);
	}
```



「**自底向上」**的意思是：从最底下，问题规模最小的`fib(1)`和`fib(2)`开始往上推，直到推到我们想要的答案`fib(4)`，这就是动态规划DP的思路。（**Bottom-up**）

```
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

###  <a href="zhuang-tai-zhuan-yi-fang-cheng" id="zhuang-tai-zhuan-yi-fang-cheng"></a>

### 状态转移方程（Governing equation）：

{% hint style="warning" %}
状态转移方程就是用**数学形式**来描述问题结构，它是解决问题的核心。
{% endhint %}

只要能写出状态转移方程，DP问题就迎刃而解。

例如：\
计算Fibonacci number的状态转移方程是 `DP[i] = DP[i-1] + DP[i-2]`；

基本的爬楼梯问题的状态转移方程是 `DP[i] = DP[i-1] + DP[i-2]`；

升级的爬楼梯问题(步数为1,2,5)状态转移方程是 `DP[i] = DP[i-1] + DP[i-2] + DP[i-5]`；



### DP的解题思路：

1. 先想brute force；
2. 思考题目的子问题是什么；
3. 通过子问题，总结出状态转移方程。



### 经典例题：

{% content-ref url="fei-bo-na-qi-shu-lie-fibonacci-number.md" %}
[fei-bo-na-qi-shu-lie-fibonacci-number.md](fei-bo-na-qi-shu-lie-fibonacci-number.md)
{% endcontent-ref %}

{% content-ref url="leetcode-70.-climbing-stairs.md" %}
[leetcode-70.-climbing-stairs.md](leetcode-70.-climbing-stairs.md)
{% endcontent-ref %}

{% content-ref url="leetcode-518.-coin-change-2.md" %}
[leetcode-518.-coin-change-2.md](leetcode-518.-coin-change-2.md)
{% endcontent-ref %}

{% content-ref url="leetcode-53.-maximum-subarray.md" %}
[leetcode-53.-maximum-subarray.md](leetcode-53.-maximum-subarray.md)
{% endcontent-ref %}

{% content-ref url="../leetcode/leetcode-121.-best-time-to-buy-and-sell-stock/leetcode-123.-best-time-to-buy-and-sell-stock-iii.md" %}
[leetcode-123.-best-time-to-buy-and-sell-stock-iii.md](../leetcode/leetcode-121.-best-time-to-buy-and-sell-stock/leetcode-123.-best-time-to-buy-and-sell-stock-iii.md)
{% endcontent-ref %}



64\. Minimum Path Sum





