## 解法

### 方法一：动态规划

dp[i][0] 表示第 i 天交易完后手里没有股票的最大利润

dp[i][1] 表示第 i 天交易完后手里持有一支股票的最大利润

prices[i] 当前股价

那么dp[i][0]，情况等于：前一天没有股票（已卖出），或者今天卖出股票

dp[i][0] = max(dp[i-1][0], dp[i - 1][1] + prices[i])

dp[i][1]，表示当天手里有股票的最大利润，情况等于：前一天有股票的最大利润，或则今天买入股票(只能买卖一次，所以肯定是前一天没有股票)

dp[i][1] = max(dp[i-1][1], dp[i - 1][0] - prices[i])

由题可知：第一天：dp[0][0] = 0， dp[0][1] = -prices[0] （第一天股票价格）


```
var maxProfit = function(prices) {
    const tradeDay = prices.length;
    const calendar = new Array(tradeDay).fill([0, 0])
    calendar[0][0] = 0 // 初始化第一天 没有股票肯定没钱
    calendar[0][1] = -prices[0] // 第一天买了 就负债当前的股票
    for (var i = 1; i < tradeDay; i++) {
        const currentDayPrice = prices[i];
        calendar[i][0] = Math.max(calendar[i - 1][0], calendar[i - 1][1] + currentDayPrice)
        calendar[i][1] = Math.max(calendar[i - 1][1], calendar[i - 1][0] - currentDayPrice)
    }
    return calendar[tradeDay - 1][0]
};
```

### 方法二：贪心

![](https://epiboly-1256208535.cos.ap-chengdu.myqcloud.com/algorithm/clipboard_20201112020731.png)

```
var maxProfit = function(prices) {
    let ans = 0;
    let n = prices.length;
    for (let i = 1; i < n; ++i) {
        ans += Math.max(0, prices[i] - prices[i - 1]);
    }
    return ans;
};
```