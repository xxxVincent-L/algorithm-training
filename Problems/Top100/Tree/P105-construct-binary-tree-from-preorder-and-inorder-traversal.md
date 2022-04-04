# [105\. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

## Descriptions:
Difficulty: **Medium**


给定两个整数数组 `preorder` 和 `inorder` ，其中 `preorder` 是二叉树的**先序遍历**， `inorder` 是同一棵树的**中序遍历**，请构造二叉树并返回其根节点。

**示例 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/tree.jpg)

```
输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
输出: [3,9,20,null,null,15,7]
```

**示例 2:**

```
输入: preorder = [-1], inorder = [-1]
输出: [-1]
```

**提示:**

*   `1 <= preorder.length <= 3000`
*   `inorder.length == preorder.length`
*   `-3000 <= preorder[i], inorder[i] <= 3000`
*   `preorder` 和 `inorder` 均 **无重复** 元素
*   `inorder` 均出现在 `preorder`
*   `preorder` **保证** 为二叉树的前序遍历序列
*   `inorder` **保证** 为二叉树的中序遍历序列


## Solutions:

Language: **C++**

```c++
​/**
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
    unordered_map<int, int> map;
    TreeNode* build(vector<int>& preorder, int preStart, int preEnd,vector<int>& inorder, int inStart, int inEnd){
        //1. 递归出口 临界条件
        if(preStart > preEnd)
             return  nullptr;

        //2. 变量定义

        int rootVal = preorder[preStart];
        int index = 0;

        for(int i = inStart;i<=inEnd;i++){
            if(rootVal == inorder[i])
                index = i;
        }
        int leftSize = index - inStart;



        //3. 进行递归
        TreeNode* root = new TreeNode(rootVal);

        root->left = build(preorder,preStart+1,preStart+leftSize,inorder,inStart,index-1);
        root->right = build(preorder,preStart+leftSize+1,preEnd,inorder,index+1,inEnd);

        return root;

    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {

        return build(preorder,0,preorder.size()-1,inorder,0,inorder.size()-1);

    }
};
```


## Summary:
