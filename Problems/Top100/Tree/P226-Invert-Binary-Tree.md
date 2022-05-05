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
其实还是得看这个

二叉树类的题目大致可以分成两种：
* **是否可以通过遍历一遍二叉树得到答案？** 如果可以，用一个 traverse 函数配合外部变量来实现。
* **是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案？** 如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值。

无论使用哪一种思维模式，你都要明白:**单独抽出一个二叉树节点,这个节点需要做什么，需要在什么时候（前中后序）做**.

本题中的镜像本质上就是使用**结点的交换**，注意这里是结点的交换，而不是值的交换，刚开始时我的思路有点跑偏，搞成值的交换。但细细想一下就会发现，完成该层结点的交换后，到下一层就无法对调两个不同子树的值，只能改变子树里的值了。

并且本体我采用了**第一个思路**。遍历了整棵树！相当于在先序的位置完成了处理！
