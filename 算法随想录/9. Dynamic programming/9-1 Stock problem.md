## [123. Best Time to Buy and Sell Stock III](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/)
dp[i][0] the second number is how many transaction we make(buy or sell)

Noticed that dp[0][3] is -prices[0] since we can buy sell at day 0th and then buy again;
```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(),vector<int>(5,0));
        dp[0][1] = -prices[0];
        dp[0][3] = -prices[0];
        for(int i = 1; i<prices.size(); i++){
            dp[i][0] = dp[i-1][0];
            dp[i][1] = max(dp[i-1][1],-prices[i]);
            dp[i][2] = max(dp[i-1][2],dp[i-1][1]+prices[i]);
            dp[i][3] = max(dp[i-1][3],dp[i-1][2]-prices[i]);
            dp[i][4] = max(dp[i-1][4],dp[i-1][3]+prices[i]); 
        }
        return max({dp.back()[2],dp.back()[4]});
    }
};
```

3D solution
```CPP
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<vector<long long>>> dp(prices.size(), vector<vector<long long>>(2, vector<long long>(3, 0)));
            dp[0][1][0] = -prices[0];
            dp[0][0][1] = INT_MIN;
            dp[0][1][1] = INT_MIN;
            dp[0][0][2] = INT_MIN;
        for(int i = 1; i<prices.size(); i++){
            dp[i][0][0] = dp[i-1][0][0];
            dp[i][1][0] = max(dp[i-1][1][0],dp[i-1][0][0]-prices[i]);
            dp[i][0][1] = max(dp[i-1][0][1],dp[i-1][1][0]+prices[i]);
            dp[i][1][1] = max(dp[i-1][1][1],dp[i-1][0][1]-prices[i]);
            dp[i][0][2] = max(dp[i-1][0][2],dp[i-1][1][1]+prices[i]);
        }
        return max({dp.back()[0][0], dp.back()[0][1], dp.back()[0][2]});
    }
};
```

## [188. Best Time to Buy and Sell Stock IV](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/)
Similar to the above one but just use loop to generate each j status
```CPP
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        vector<vector<int>> dp(prices.size(),vector<int>(2*k+1,0));
        for(int i = 1; i<2*k+1; i++){
            if(i%2!=0) dp[0][i] = -prices[0];
        }
        for(int i = 1; i<prices.size(); i++){
            for(int j = 1; j<2*k+1; j++){
                dp[i][j] = j % 2 == 0 ? max(dp[i-1][j], dp[i-1][j-1] + prices[i]) : max(dp[i-1][j], dp[i-1][j-1] - prices[i]);

            }
        }
        int result = 0;
        for(int profit:dp.back()){
            result = max(result,profit);
        }
        return result;
    }
};
```
