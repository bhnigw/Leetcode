# \[Leetcode\]122. Best Time to Buy and Sell Stock II

原题地址：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

题意：在给出的时间段内，不限交易次数，求能获得的最大股票收益。

![](../.gitbook/assets/122_maxprofit_1.png)

### 算法：

股票的性质，只要买了之后在涨，那都是在赚钱的；

所以，找出input数组内所有的单调递增区间，然后求和即可；

```text
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        int res = 0;
        
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] > prices[i - 1])
                res += prices[i] - prices[i - 1];
        }
        
        return res;
    }
}
```

Time: O\(n\);

Space: O\(1\);









