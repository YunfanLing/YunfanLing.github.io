## [647. Palindromic Substrings](https://leetcode.cn/problems/palindromic-substrings/description/)
Based on the property of palindromic string, build the string from a simple char, then larger it on both side front and end, check front==end? 
Recursion can based on vector like below.

![image](https://github.com/YunfanLing/YunfanLing.github.io/assets/102476857/1196373c-4d84-4e0f-8819-529383c1bba3)


```CPP
class Solution {
public:
    int countSubstrings(string s) {
        vector<vector<bool>> dp(s.size(),vector<bool>(s.size(),0));
        int result = 0;
        for(int i = s.size()-1; i>=0; i--){
            for(int j = i; j<s.size(); j++){
                if(s[i]==s[j]){
                    if(j-i<=1){
                        dp[i][j] = 1;
                        result++;
                    }else{
                        dp[i][j] = dp[i+1][j-1];
                        if(dp[i][j]) result++;
                    }
                }
            }
        }
        return result;
    }
};
```

## [516. Longest Palindromic Subsequence](https://leetcode.cn/problems/longest-palindromic-subsequence/description/)
When s[i]!=s[j] we can get dp from without i and without j which is larger.
```CPP
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        vector<vector<int>> dp(s.size(),vector<int>(s.size(),0));
        for(int i = s.size()-1; i>=0; i--){
            for(int j = i; j<s.size(); j++){
                if(s[i]==s[j]){
                    if(i==j) dp[i][j] = 1;
                    else dp[i][j] = dp[i+1][j-1]+2;
                }
                else dp[i][j] = max(dp[i+1][j],dp[i][j-1]);
            }
        }
        return dp[0][s.size()-1];
    }
};
```
return dp[0][s.size()-1]; this is what we return
