# [144\. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

## Descriptions:
Difficulty: **Easy**


给你二叉树的根节点 `root` ，返回它节点值的 **前序**遍历。

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_1.jpg)

```
输入：root = [1,null,2,3]
输出：[1,2,3]
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

**示例 4：**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_5.jpg)

```
输入：root = [1,2]
输出：[1,2]
```

**示例 5：**

![](https://assets.leetcode.com/uploads/2020/09/15/inorder_4.jpg)

```
输入：root = [1,null,2]
输出：[1,2]
```

**提示：**

*   树中节点数目在范围 `[0, 100]` 内
*   `-100 <= Node.val <= 100`

**进阶:** 递归算法很简单，你可以通过迭代算法完成吗？


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
        vector<int> res;


    void traverse(TreeNode* root, vector<int>& res){

        if(root == nullptr) return ;

        res.push_back(root->val);
        traverse(root->left,res);

        traverse(root->right,res);


    }

    vector<int> preorderTraversal(TreeNode* root) {

        traverse(root, res);

        return res;

    }
};
​
```
## Summary:
