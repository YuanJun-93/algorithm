#### [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 `n` ，求斐波那契（Fibonacci）数列的第 `n` 项（即 `F(N)`）。斐波那契数列的定义如下：

```
F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
```

斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

**示例 1：**

```
输入：n = 2
输出：1
```

**示例 2：**

```
输入：n = 5
输出：5
```

**提示：**

- `0 <= n <= 100`

C++

递归超时

```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0){
            return 0;
        }
        if(n == 1){
            return 1;
        }
        return (fib(n-1) + fib(n-2))%1000000007;
    }
};
```

记忆化搜索

```c++
class Solution {
public:
    int mod = 1000000007;
    vector<int> mem;
    int fib(int n) {
        mem.resize(n+1, 0);
        return fib_r(n);
    }
    int fib_r(int n){
        if(n == 0) return 0;
        if(n == 1) return 1;
        if(mem[n] != 0){
            return mem[n];
        }
        mem[n] = (fib_r(n-1) + fib_r(n-2)) % mod;
        return mem[n];
    }
};
```