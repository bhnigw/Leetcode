---
description: Dynamic Programming，DP
---

# \[Leetcode\]518. Coin Change 2

原题地址：[https://leetcode.com/problems/coin-change-2/](https://leetcode.com/problems/coin-change-2/) 关键词：Dynamic Programming，DP

题意：给一个数组 coins 表示不同面额的硬币，给一个整数 amount 表示总金额；计算可以凑amount金额方法总数。如果任何硬币组合都无法凑出总金额，返回 0 。

例：  
Input: `amount = 5, coins = [1,2,5]`   
Output: 4   
解释：有以下四种方式可以凑成总金额5：  
5=5   
5=2+2+1   
5=2+1+1+1   
5=1+1+1+1+1

### 算法：Dynamic Programming



初始化`dp[0] = 1`；遍历`coins[]`，对于其中的每个元素coin，进行如下操作：

遍历 ii 从 \textit{coin}coin 到 \textit{amount}amount，将 \textit{dp}\[i - \textit{coin}\]dp\[i−coin\] 的值加到 \textit{dp}\[i\]dp\[i\]。 最终得到 \textit{dp}\[\textit{amount}\]dp\[amount\] 的值即为答案。





