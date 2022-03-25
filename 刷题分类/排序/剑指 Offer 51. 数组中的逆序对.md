#### [剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

**示例 1:**

```
输入: [7,5,6,4]
输出: 5
```

**限制：**

```
0 <= 数组长度 <= 50000
```

C++

```c++
class Solution {
public:
    int reverseCount = 0;
    int reversePairs(vector<int>& nums) {
        mergeSort(nums, 0, nums.size() - 1);
        return reverseCount;
    }
    void mergeSort(vector<int>& nums, int p, int r) {
        if (p >= r) return;
        int q = (p + r) / 2;
        mergeSort(nums, p, q);
        mergeSort(nums, q + 1, r);
        merge(nums, p, q, r);
    }
    int merge(vector<int>& nums, int p, int q, int r) {
        vector<int> tmp(r - p + 1);
        int i = p;
        int j = q + 1;
        int k = 0;
        while (i <= q && j <= r) {
            if (nums[j] < nums[i]) {
                reverseCount += (q - i + 1);
                tmp[k++] = nums[j];
                j++;
            } else {
                tmp[k++] = nums[i];
                i++;
            }
        }
        while (j <= r) {
            tmp[k++] = nums[j];
            j++;
        }
        while (i <= q) {
            tmp[k++] = nums[i];
            i++;
        }
        for (int i = 0; i < r - p + 1; ++i) {
            nums[i + p] = tmp[i];
        }
        return reverseCount;
    }
};
```

