# [102\. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

## Descriptions:

Difficulty: **Easy**


给你二叉树的根节点 `root` ，返回其节点值的 **层序遍历** 。 （即逐层地，从左到右访问所有节点）。

**示例 1：**

![](https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg)

```
输入：root = [3,9,20,null,null,15,7]
输出：[[3],[9,20],[15,7]]
```

**示例 2：**

```
输入：root = [1]
输出：[[1]]
```

**示例 3：**

```
输入：root = []
输出：[]
```

**提示：**

*   树中节点数目在范围 `[0, 2000]` 内
*   `-1000 <= Node.val <= 1000`


## Solutions:

Language: **C++**

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        //1. 变量定义
        vector<vector<int>> res;

        queue<TreeNode*> q;
        if(root)
            q.push(root);

        while(!q.empty()){
            int size = q.size();
            vector<int> vec;
            for(int i = 0; i < size; i++){
                TreeNode* temp = q.front();
                q.pop();

                vec.push_back(temp->val);

                if(temp->left!=nullptr) q.push(temp->left);
                if(temp->right!=nullptr) q.push(temp->right);

            }
            res.push_back(vec);
        }

        return res;
    }
};
​
```

## Summary:
