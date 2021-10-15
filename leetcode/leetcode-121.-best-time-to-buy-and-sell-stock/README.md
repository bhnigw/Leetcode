# \[Leetcode]121. Best Time to Buy and Sell Stock

原题地址：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

题意：在给出的时间段内只交易一次（买进一次，卖出一次），求能获得的最大股票收益。

例：\
`Input: prices = [7,1,5,3,6,4] `\
`Output: 5`\
解释：在股价为1的时候买进，股价为6的时候卖出；

![](../../.gitbook/assets/121\_profit_graph.png)

### 算法：

要获得的最大股票收益，就要最低点买进，最高点卖出；

要符合卖出的条件，就要**保证最高的点出现在最低的点的右边**，才能够成功卖出。

具体做法就是：在左边找到最低点minPrice，然后右边每一个点都和minPrice减一遍，求其中的最大值；

```
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) return 0;
        
        int minPrice = prices[0]; // 注意初始值
        int profit = 0;
        
        for (int i = 1; i < prices.length; i++) { // i从1开始
            minPrice = Math.min(prices[i], minPrice); //时刻更新最小值
            if (prices[i] > minPrice) {
                profit = Math.max(prices[i] - minPrice, profit); //在最小值的右边更新最大值
            }
        }
        
        return profit;
    }
}
```

Time: O(n);

Space: O(1);
