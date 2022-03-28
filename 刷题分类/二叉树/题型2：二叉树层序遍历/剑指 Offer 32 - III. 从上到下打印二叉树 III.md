#### [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [20,9],
  [15,7]
]
```

**提示：**

1. `节点总数 <= 1000`



C++

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if(root == NULL){
            return res;
        }
        vector<stack<TreeNode*>> vec(2);
        int turn = 0;
        vec[turn].push(root);
        while(!vec[turn].empty()){
            vector<int> tmp;
            int size = vec[turn].size();
            while(size--){
                TreeNode *node = vec[turn].top();
                vec[turn].pop();
                tmp.push_back(node->val);
                if(turn == 0){
                    if(node->left != NULL){
                        vec[1].push(node->left);
                    }
                    if(node->right != NULL){
                        vec[1].push(node->right);
                    }
                }else{
                    if(node->right != NULL){
                        vec[0].push(node->right);
                    }
                    if(node->left != NULL){
                        vec[0].push(node->left);
                    }
                }
            }
            turn = (turn + 1) % 2;
            res.push_back(tmp);
        }
        return res;
    }
};
```

