# [226\. 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

## Descriptions:
Difficulty: **Easy**


给你一棵二叉树的根节点 `root` ，翻转这棵二叉树，并返回其根节点。

**示例 1：**

![](https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg)

```
输入：root = [4,2,7,1,3,6,9]
输出：[4,7,2,9,6,3,1]
```

**示例 2：**

![](https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg)

```
输入：root = [2,1,3]
输出：[2,3,1]
```

**示例 3：**

```
输入：root = []
输出：[]
```

**提示：**

*   树中节点数目范围在 `[0, 100]` 内
*   `-100 <= Node.val <= 100`


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
    void traverse(TreeNode* root){
        if(root == nullptr)
            return ;
        // swap(root->left->val, root->right->val);
        // 是整个结点都需要交换噢！
        TreeNode* tmp;
        tmp = root->left;
        root->left = root->right;
        root->right = tmp;
        traverse(root->left);
        traverse(root->right);
    }
    TreeNode* invertTree(TreeNode* root) {


        traverse(root);
        return root;
    }
};
​
```

## Summary:
