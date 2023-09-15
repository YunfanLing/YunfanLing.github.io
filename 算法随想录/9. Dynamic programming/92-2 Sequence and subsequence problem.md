## [1143. Longest Common Subsequence](https://leetcode.cn/problems/longest-common-subsequence/)
![image](https://github.com/YunfanLing/YunfanLing.github.io/assets/102476857/8612505e-208f-49fa-9130-e0522dfa1a44)
If the condition nums1[i-1]==nums2[j-1] the dp[i][j] derive from the left upper

Else it derives from the larger one from the upper and left

```CPP
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        vector<vector<int>> dp(text1.size()+1,vector<int>(text2.size()+1,0));
        int result = 0;
        for(int i = 1; i<=text1.size(); i++){
            for(int j = 1; j<=text2.size();j++){
                if(text1[i-1]==text2[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                else dp[i][j] = max(dp[i][j-1],dp[i-1][j]);
                result = max(result,dp[i][j]);
            }
        }
        return result;
    }
};
```

## [1035. Uncrossed Lines](https://leetcode.cn/problems/uncrossed-lines/)
Just draw a map we will find this question is same like the previous one.
```CPP
class Solution {
public:
    int maxUncrossedLines(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>> dp(nums1.size()+1,vector<int>(nums2.size()+1,0));
        int result = 0;
        for(int i = 1; i<=nums1.size(); i++){
            for(int j = 1; j<=nums2.size();j++){
                if(nums1[i-1]==nums2[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                else dp[i][j] = max(dp[i-1][j],dp[i][j-1]);
                result = max(result,dp[i][j]);
            }
        }
        return result;
    }
};
```

## [53. Maximum Subarray](https://leetcode.cn/problems/maximum-subarray/)
```CPP
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums.begin(),nums.end());
        int result = nums[0];
        for(int i = 1; i<nums.size(); i++){
            dp[i] = max(dp[i],dp[i-1]+nums[i]);
            result = max(result,dp[i]);
        }
        return result;
    }
};
```
