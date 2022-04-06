#### [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个m行n列的方格，从坐标 `[0,0]` 到坐标 `[m-1,n-1]` 。一个机器人从坐标 `[0, 0] `的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

 

**示例 1：**

```
输入：m = 2, n = 3, k = 1
输出：3
```

**示例 2：**

```
输入：m = 3, n = 1, k = 0
输出：1
```

**提示：**

- `1 <= n,m <= 100`
- `0 <= k <= 20`



C++

```c++
class Solution {
public:
    int count = 0;
    vector<vector<bool>> visited;
    int movingCount(int m, int n, int k) {
        visited.assign(m, vector<bool>(n));
        dfs(0, 0, m, n, k);
        return count;
    }
    void dfs(int i, int j, int m, int n, int k){
        visited[i][j] = true;
        count++;
        vector<vector<int>> dir = {{1, 0}, {-1, 0}, {0, -1}, {0, 1}};
        for(int d = 0; d < 4; d++){
            int dx = i + dir[d][0];
            int dy = j + dir[d][1];
            if(dx >= m || dx < 0 || dy >= n || dy < 0 ||
            visited[dx][dy] == true || check(dx, dy, k) == false){
                continue;
            }
            dfs(dx, dy, m, n, k);
        }
    }
    bool check(int x, int y, int k){
        int sum = 0;
        while(x > 0){
            sum += x % 10;
            x /= 10;
        }
        while(y > 0){
            sum += y % 10;
            y /= 10;
        }
        return sum <= k;
    }
};
```

