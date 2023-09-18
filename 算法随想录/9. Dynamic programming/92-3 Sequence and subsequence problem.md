## [392. Is Subsequence](https://leetcode.cn/problems/is-subsequence/)
Method 1: dp[i][j] length of the same char in [0,i-1],[0,j-1]
```CPP
class Solution {
public:
    bool isSubsequence(string s, string t) {
        //using length of the same char is more efficient
        vector<vector<int>> dp(s.size()+1,vector<int>(t.size()+1,0));
        for(int i = 1; i<=s.size(); i++){
            for(int j = 1; j<=t.size(); j++){
                if(s[i-1]==t[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                else dp[i][j] = dp[i][j-1];
            }
        }
        return (dp.back().back()==s.size());
    }
};
```

Method 2: dp[i][j] whether [j-1] is the subsequence of [i-1]
```CPP
class Solution {
public:
    bool isSubsequence(string s, string t) {
        vector<vector<bool>> dp(s.size()+1,vector<bool>(t.size()+1,0));
        for(int i = 0; i<=t.size(); i++){
            dp[0][i] = 1;
        }
        for(int i = 1 ;i<=s.size(); i++){
            for(int j = 1; j<=t.size(); j++){
                if(s[i-1]==t[j-1]) dp[i][j] = dp[i-1][j-1];
                else dp[i][j] = dp[i][j-1];
                cout<<dp[i][j]<<" ";
            }
            cout<<endl;
        }
        return dp.back().back();
    }
};
```

## [115. Distinct Subsequences](https://leetcode.cn/problems/distinct-subsequences/)
dp[i][j] how many distinct subsequence we have in s can equal to t(our target)

Recursion equation: if s[j-1]==t[i-1] dp[i][j] = subsequences have s[j-1] dp[i-1][j-1] + subsequence not have s[j-1] but equal to t[0,i-1] which is dp[i][j-1];
![image](https://github.com/YunfanLing/YunfanLing.github.io/assets/102476857/7a5e3617-e526-43ff-97b5-12039b2908ae)

```CPP
class Solution {
public:
    int numDistinct(string s, string t) {
        vector<vector<uint64_t>> dp(t.size()+1,vector<uint64_t>(s.size()+1,0));
        for(int i = 1; i<=s.size();i++){
            if(t[0]==s[i-1]) dp[1][i] = dp[1][i-1]+1;
            else dp[1][i] = dp[1][i-1];
            //cout<<dp[1][i]<<" "; 
        }
        //cout<<endl;
        for(int i = 2; i<=t.size(); i++){
            for(int j = 2; j<=s.size();j++){
                if(t[i-1]==s[j-1]) dp[i][j] = dp[i-1][j-1]+dp[i][j-1];
                else dp[i][j] = dp[i][j-1];
                //cout<<dp[i][j]<<" ";
            }
            //cout<<endl;
        }
        return dp.back().back();
    }
};
```
