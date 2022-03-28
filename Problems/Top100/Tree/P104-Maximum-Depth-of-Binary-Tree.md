# [104\. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

## Descriptions:
Difficulty: **Easy**


给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

**示例：**
给定二叉树 `[3,9,20,null,null,15,7]`，

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。


## Solutions:

Language: **C++**

* Sol1
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
    int res = 0;
    int dep = 0;
    void traverse(TreeNode* root){

        if(root == nullptr){
            res = max(res, dep);
            return;
        }
        dep++;
        traverse(root->left);
        traverse(root->right);
        dep--;
    }
    int maxDepth(TreeNode* root) {
        traverse(root);
        return res;
    }
};
​
```

* Sol2

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

    int maxDepth(TreeNode* root) {
        if(root == nullptr) return 0;

        int leftMax = maxDepth(root->left);
        int rightMax = maxDepth(root->right);

        int res = max(leftMax,rightMax)+1;

        return res;
    }
};
```
## Summary:

二叉树类的题目大致可以分成两种：
* **是否可以通过遍历一遍二叉树得到答案？** 如果可以，用一个 traverse 函数配合外部变量来实现。
* **是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案？** 如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。

无论使用哪一种思维模式，你都要明白:**单独抽出一个二叉树节点,这个节点需要做什么，需要在什么时候（前中后序）做**.
