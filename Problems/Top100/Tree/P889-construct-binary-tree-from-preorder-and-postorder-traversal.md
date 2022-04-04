# [889\. 根据前序和后序遍历构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal/)

## Descriptions：
Difficulty: **Medium**


给定两个整数数组，`preorder` 和 `postorder` ，其中 `preorder` 是一个具有 **无重复** 值的二叉树的前序遍历，`postorder` 是同一棵树的后序遍历，重构并返回二叉树。

如果存在多个答案，您可以返回其中 **任何** 一个。

**示例 1：**

![](https://assets.leetcode.com/uploads/2021/07/24/lc-prepost.jpg)

```
输入：preorder = [1,2,4,5,3,6,7], postorder = [4,5,2,6,7,3,1]
输出：[1,2,3,4,5,6,7]
```

**示例 2:**

```
输入: preorder = [1], postorder = [1]
输出: [1]
```

**提示：**

*   `1 <= preorder.length <= 30`
*   `1 <= preorder[i] <= preorder.length`
*   `preorder` 中所有值都 **不同**
*   `postorder.length == preorder.length`
*   `1 <= postorder[i] <= postorder.length`
*   `postorder` 中所有值都 **不同**
*   保证 `preorder` 和 `postorder` 是同一棵二叉树的前序遍历和后序遍历


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
    unordered_map<int,int> postorder_index;
    TreeNode* build(vector<int>& preorder, int preStart, int preEnd,vector<int>& postorder, int postStart, int postEnd){

        if(preStart> preEnd)
            return nullptr;
        int rootVal = preorder[preStart];
        TreeNode* root = new TreeNode(rootVal);
        if(preStart == preEnd)
            return root;
        int index = 0;

        int leftRootVal = preorder[preStart+1];

        // 这里的循环我写出问题了...
        for(int i = postStart; i<= postEnd;i++){
            if(leftRootVal == postorder[i]){
                index = i;
            }
        }
        int leftSize = index - postStart + 1;

        root->left = build(preorder,preStart+1,preStart+leftSize,postorder,postStart,index);
        root->right = build(preorder,preStart+leftSize+1,preEnd,postorder,index+1,postEnd-1);
        return root;
    }
    TreeNode* constructFromPrePost(vector<int>& preorder, vector<int>& postorder) {

        return build(preorder,0,preorder.size()-1,postorder,0,postorder.size()-1);
    }
};
​
```

## Summary:
