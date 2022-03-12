## [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

**示例1：**

```
输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

**限制：**

```
0 <= 链表长度 <= 1000
```

注意：本题与主站 21 题相同：https://leetcode-cn.com/problems/merge-two-sorted-lists/

C++

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        if(l1 == NULL){
            return l2;
        }
        if(l2 == NULL){
            return l1;
        }
        ListNode *p1 = l1;
        ListNode *p2 = l2;
        ListNode *dummy = new ListNode(-1);
        ListNode *tail = dummy;
        while(p1 && p2){
            if(p1->val <= p2->val){
                tail->next = p1;
                tail = p1;
                p1 = p1->next;
            }else{
                tail->next = p2;
                tail = p2;
                p2 = p2->next;
            }
        }
        if(p1){
            tail->next = p1;
        }
        if(p2){
            tail->next = p2;
        }
        return dummy->next;
    }
};
```