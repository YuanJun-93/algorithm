#### [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

**示例 1**

```
输入：x = 2.00000, n = 10
输出：1024.00000
```

**示例 2：**

```
输入：x = 2.10000, n = 3
输出：9.26100
```

**示例 3：**

```
输入：x = 2.00000, n = -2
输出：0.25000
解释：2-2 = 1/22 = 1/4 = 0.25
```

**提示：**

- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `-104 <= xn <= 104`

 C++

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if(n >= 0) return rPow(x, n);
        else return 1/(rPow(x, -1*(n+1))*x);
    }
    double rPow(double x, int n){
        if(n == 0) return 1;
        double halfPow = rPow(x, n/2);
        if(n % 2 == 1){
            return halfPow * halfPow * x;
        }else{
            return halfPow * halfPow;
        }
    }
};
```