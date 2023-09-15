## [300. Longest Increasing Subsequence](https://leetcode.cn/problems/longest-increasing-subsequence/)
dp[i] here largest subsequence including i in [0,i]

Not continues
```CPP
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> dp(nums.size(),1); //largest subsequence incluing i
        for(int i = 0; i<nums.size();i++){
            for(int j = 0; j<i;j++){
                if(nums[j]<nums[i]) dp[i] = max(dp[i],dp[j]+1);
            }
        }
        int result = 0;
        for(int i = 0; i<dp.size();i++){
            result = max(result,dp[i]);
        }
        return result;
    }
};
```

## [674. Longest Continuous Increasing Subsequence](https://leetcode.cn/problems/longest-continuous-increasing-subsequence/)
It is continuous.
```CPP
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        vector<int> dp(nums.size(),1);

        for(int i = 1;i<nums.size();i++){
            if(nums[i]>nums[i-1]) dp[i] = dp[i-1]+1;
        }
        int result = 0;
        for(int num:dp){
            result = max(result,num);
        }
        return result;
    }
};
```

## [718. Maximum Length of Repeated Subarray](https://leetcode.cn/problems/maximum-length-of-repeated-subarray/)
dp[i][j] means the largest repeated subarray in [0,i-1] and[0,j-1] not i and j since it is easier to initialize the DP in this way.

It is continuous

![image](https://github.com/YunfanLing/YunfanLing.github.io/assets/102476857/250177de-96b9-49ae-8efd-0cb38ee894af)

```CPP
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>> dp(nums1.size()+1,vector<int>(nums2.size()+1,0));
        int result = 0;
        for(int i = 1; i<=nums1.size(); i++){
            for(int j = 1; j<=nums2.size();j++){
                if(nums1[i-1]==nums2[j-1]) dp[i][j] = dp[i-1][j-1]+1;
                result = max(result,dp[i][j]);
            }
        }
        return result;
    }
};
```

