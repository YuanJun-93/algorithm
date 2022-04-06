#### [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

 

**示例 1:**

```
输入: 12258
输出: 5
解释: 12258有5种不同的翻译，分别是"bccfi", "bwfi", "bczi", "mcfi"和"mzi"
```

 

**提示：**

- `0 <= num < 231`



C++

```c++
class Solution {
public:
    int translateNum(int num) {
        if(num <= 9) return 1;
        vector<int> digits;
        while(num){
            digits.push_back(num % 10);
            num /= 10;
        }
        int n = digits.size();
        reverse(digits.begin(), digits.end());
        vector<int> dp(n + 1);
        dp[0] = 1;
        for(int i = 1; i <= n; i++){
            dp[i] = dp[i - 1];
            if(i - 2 >= 0 && isValid(digits[i - 2], digits[i - 1])){
                dp[i] += dp[i - 2];
            }
        }
        return dp[n];
    }
    bool isValid(int a, int b){
        if(a == 1) return true;
        if(a == 2 && b >= 0 && b <= 5) return true;
        return false;
    }
};
```

