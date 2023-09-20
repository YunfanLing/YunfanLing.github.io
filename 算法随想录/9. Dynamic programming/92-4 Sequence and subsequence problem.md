## [583. Delete Operation for Two Strings](https://leetcode.cn/problems/delete-operation-for-two-strings/)
Another thinking is find the largest common subsequence number m, so that the operation can be w1.size+w2.size-2m.
```CPP
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>>dp(word1.size()+1,vector<int>(word2.size()+1,0));
        for(int i = 1; i<=word2.size(); i++){
            dp[0][i] = i;
        }
        for(int j = 1; j<=word1.size();j++){
            dp[j][0] = j;
        }
        for(int i = 1; i<=word1.size(); i++){
            for(int j = 1; j<=word2.size(); j++){
                if(word1[i-1]==word2[j-1]) dp[i][j] = dp[i-1][j-1];
                else dp[i][j] = min(dp[i-1][j]+1, dp[i][j-1]+1);
                //cout<<dp[i][j]<<" ";
            }
            //cout<<endl;
        }
        return dp.back().back();
    }
};
```

## [72. Edit Distance](https://leetcode.cn/problems/edit-distance/description/)
We can regard insertion and deletion as the same thing, here we only consider insertion but separately on w1 and w2(and we can also manipulate word1 and word2). w1 insert simulate w2 delete, w2 insert is w2 insert
If w1[i-1] and w2[j-1] are not the same we compare three operations which has the lowest value:

1. From dp[i-1][j-1] we replace 1 to make the same: that is dp[i-1][j-1]+1

2. From dp[i-1][j] we insert 1 to w1 to make the same: that is dp[i-1][j]+1
   
3. From dp[i][j-1] we insert 1 to w2 to make the same: that is dp[i][j-1]+1
 
The below w1 and w2 is different than above
```CPP
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word2.size()+1,vector<int>(word1.size()+1,0));
        for(int i = 0; i<=word2.size(); i++){
            dp[i][0] = i;
        }
        for(int j = 0; j<=word1.size(); j++){
            dp[0][j] = j;
        }
        for(int i = 1; i<=word2.size(); i++){
            for(int j = 1; j<=word1.size(); j++){
                if(word2[i-1]==word1[j-1]) dp[i][j] = dp[i-1][j-1];
                else{
                    dp[i][j] = min({dp[i-1][j-1]+1,dp[i][j-1]+1,dp[i-1][j]+1});
                }
                //cout<<dp[i][j]<<" ";
            }
            //cout<<endl;
        }
        return dp.back().back();
    }
};
```
