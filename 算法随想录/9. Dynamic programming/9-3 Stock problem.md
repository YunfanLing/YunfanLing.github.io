##  [309. Best Time to Buy and Sell Stock with Cooldown](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/)
Add more status in the dp array

Initialization can depend on the recuresion equation
```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(),vector<int>(4,0));
        dp[0][1] = -prices[0];
        for(int i = 1; i<prices.size(); i++){
            dp[i][0] = max(dp[i-1][0],dp[i-1][3]);
            dp[i][1] = max({dp[i-1][1],dp[i-1][0]-prices[i],dp[i-1][3]-prices[i]});
            dp[i][2] = dp[i-1][1]+prices[i];
            dp[i][3] = dp[i-1][2];
        }
        return max({dp.back()[0],dp.back()[2],dp.back()[3]});
    }
};
```

## [714. Best Time to Buy and Sell Stock with Transaction Fee](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/)
There are only one time fee for buy and sell togather
```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        vector<vector<int>> dp(prices.size(),vector<int>(2,0));
        dp[0][1] = -prices[0];
        for(int i = 1;i<prices.size();i++){
            dp[i][0] = max(dp[i-1][0],dp[i-1][1]+prices[i]-fee);
            dp[i][1] = max(dp[i-1][1],dp[i-1][0]-prices[i]); 
        }
        return dp.back()[0];
    }
};
```
