#### [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

**限制：**

```
0 <= 链表长度 <= 10000
```

C++

递归

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        vector<int> res;
        reverseTraverl(head, res);
        return res;
    }
    void reverseTraverl(ListNode *head, vector<int> &res){
        if(head == NULL){
            return;
        }
        reverseTraverl(head->next, res);
        res.push_back(head->val);
    }
};
```

第二种递归

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    vector<int> reversePrint(ListNode* head) {
        if(head == NULL){
            return {};
        }
        vector<int> subRes = reversePrint(head->next);
        vector<int> res(subRes.size() + 1);
        for(int i = 0; i < subRes.size(); i++){
            res[i] = subRes[i];
        }
        res[res.size() - 1] = head->val;
        return res;
    }
};
```