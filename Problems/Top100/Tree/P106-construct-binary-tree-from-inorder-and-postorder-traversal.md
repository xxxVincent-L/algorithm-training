# [106\. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

## Descriptions:

Difficulty: **Medium**


给定两个整数数组 `inorder` 和 `postorder` ，其中 `inorder` 是二叉树的中序遍历， `postorder` 是同一棵树的后序遍历，请你构造并返回这颗 _二叉树_ 。

**示例 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入：inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
输出：[3,9,20,null,null,15,7]
```

**示例 2:**

```
输入：inorder = [-1], postorder = [-1]
输出：[-1]
```

**提示:**

*   `1 <= inorder.length <= 3000`
*   `postorder.length == inorder.length`
*   `-3000 <= inorder[i], postorder[i] <= 3000`
*   `inorder` 和 `postorder` 都由 **不同** 的值组成
*   `postorder` 中每一个值都在 `inorder` 中
*   `inorder` **保证**是树的中序遍历
*   `postorder` **保证**是树的后序遍历


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
    TreeNode* build(vector<int>& postorder, int postStart, int postEnd,vector<int>& inorder, int inStart, int inEnd){
        //1. 递归出口 临界条件
        if(postStart > postEnd)
             return  nullptr;

        //2. 变量定义

        int rootVal = postorder[postEnd];
        int index = 0;

        for(int i = inStart;i<=inEnd;i++){
            if(rootVal == inorder[i])
                index = i;
        }
        int leftSize = index - inStart;



        //3. 进行递归
        TreeNode* root = new TreeNode(rootVal);

        root->left = build(postorder,postStart,postStart+leftSize-1,inorder,inStart,index-1);
        root->right = build(postorder,postStart+leftSize,postEnd-1,inorder,index+1,inEnd);

        return root;

    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
            return build(postorder,0,postorder.size()-1,inorder,0,inorder.size()-1);
    }
};
​
```

## Summary:
