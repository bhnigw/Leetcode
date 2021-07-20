---
description: Fibonacci，Dynamic Programming
---

# \[Leetcode\]70. Climbing Stairs

原题地址：[https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/) 关键词：Dynamic Programming，Fibonacci

题意：爬楼梯；  
共有n个阶梯，每次可以爬1或2个台阶。问有多少种不同的方法可以爬到楼顶。







```text
class Solution {
    public int climbStairs(int n) {
        int dp[] = new int[n + 1];
        
        dp[0] = 1;  // 注意位置0的初始值是1
        dp[1] = 1;
        
        for (int i = 2; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        
        return dp[n];
    }
}
```

  


