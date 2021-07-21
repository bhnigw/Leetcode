---
description: Dynamic Programming，DP
---

# \[Leetcode\]518. Coin Change 2

原题地址：[https://leetcode.com/problems/coin-change-2/](https://leetcode.com/problems/coin-change-2/) 关键词：Dynamic Programming，DP

题意：零钱兑换；  
给一个数组`coins[]`表示不同面额的硬币，给一个整数amount表示总金额；计算可以凑amount金额方法总数。如果任何硬币组合都无法凑出总金额，返回 0 。

例：  
Input: `amount = 5, coins = [1,2,5]`   
Output: 4   
解释：有以下四种方式可以凑成总金额5：  
5 = 5   
5 = 2+2+1   
5 = 2+1+1+1   
5 = 1+1+1+1+1

### 算法：Dynamic Programming

可以用动态规划方法计算可能的组合数。用`dp[x]`表示**总额**为`x`时，硬币组合方法数，目标是求`dp[amount]`

动态规划的边界是`dp[0] = 1`；意思是，amount为0时，需要拿0枚硬币来凑总额，因此只有1种组合方法。

对于面额为coin的硬币，当`coin ≤ amount` 时，如果存在一种硬币组合的总额之和等于`amount − coin`，则在该硬币组合中增加一个面额为coin的硬币，即可得到一种金额之和等于`amount`的硬币组合。因此需要遍历coins，对于其中的每一种面额的硬币，更新数组dp中的每个大于或等于该面额的元素的值。

由此可以得到动态规划的做法：

* 初始化`dp[0] = 1`；
* 遍历`coins[]`，对于其中的每个元素coin，进行如下操作：
  * 遍历`i`从coin值到amount，将`dp[i − coin]`和`dp[i]`相加的值赋给`dp[i]`； 
* 最终得到dp\[amount\]的值即为答案；

```text
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];  //注意长度
        dp[0] = 1; 
        
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) { //注意是<=
                dp[i] = dp[i] + dp[i - coin];
            }
        }
        
        return dp[amount];
    }
}
```

Time: `O(N × amount)`, where N is a length of coins array.

Space: `O(amount)`；



