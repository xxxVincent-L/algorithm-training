# [94\. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

## Descriptions:
Difficulty: **Easy**


给定一个二叉树的根节点 `root` ，返回 _它的 **中序** 遍历_ 。

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,3,2]
```

**示例 2：**

```
输入：root = []
输出：[]
```

**示例 3：**

```
输入：root = [1]
输出：[1]
```

**提示：**

*   树中节点数目在范围 `[0, 100]` 内
*   `-100 <= Node.val <= 100`

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？


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
    void traverse(TreeNode* root, vector<int>& res){

        if(root == nullptr) return ;

        traverse(root->left,res);
        res.push_back(root->val);
        traverse(root->right,res);


    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        traverse(root, res);
        return res;

            }
};
​
```
## Summary:
