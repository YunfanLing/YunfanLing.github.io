# YunfanLing.github.io
Dailly check in for 算法随想录

## 7.26 First day

### Binary search
注意区间合法性，左闭右闭区间，条件是否可以取等号
用left+(right-left)/2 not (left+right)/2, since we will get int overflow.
How to find the left border and right border

### Remove elements
Two pointers: fast pointer for value, slow pointer for index.
