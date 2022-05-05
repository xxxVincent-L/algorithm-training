### [538\. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

Difficulty: **给出二叉 搜索 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 node 的新值等于原树中大于或等于 node.val 的值之和。 提醒一下，二叉搜索树满足下列约束条件： 节点的左子树仅包含键 小于 节点键的节点。 节点的右子树仅包含键 大于 节点键的节点。 左右子树也必须是二叉搜索树。 注意：本题和 1038: https://leetcode-cn.com/problems/binary-search-tree-to-greater-sum-tree/ 相同   示例 1： 输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8] 输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8] 示例 2： 输入：root = [0,null,1] 输出：[1,null,1] 示例 3： 输入：root = [1,0,2] 输出：[3,3,2] 示例 4： 输入：root = [3,2,4,1] 输出：[7,9,4,10]   提示： 树中的节点数介于 0 和 104 之间。 每个节点的值介于 -104 和 104 之间。 树中的所有值 互不相同 。 给定的树为二叉搜索树。 **


给出二叉 **搜索** 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 `node` 的新值等于原树中大于或等于 `node.val` 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

*   节点的左子树仅包含键 **小于** 节点键的节点。
*   节点的右子树仅包含键 **大于** 节点键的节点。
*   左右子树也必须是二叉搜索树。

**注意：**本题和 1038:  相同

**示例 1：**

**![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/05/03/tree.png)**

```
输入：[4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
输出：[30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
```

**示例 2：**

```
输入：root = [0,null,1]
输出：[1,null,1]
```

**示例 3：**

```
输入：root = [1,0,2]
输出：[3,3,2]
```

**示例 4：**

```
输入：root = [3,2,4,1]
输出：[7,9,4,10]
```

**提示：**

*   树中的节点数介于 `0` 和 `10<sup>4</sup>`之间。
*   每个节点的值介于 `-10<sup>4</sup>` 和 `10<sup>4</sup>` 之间。
*   树中的所有值 **互不相同** 。
*   给定的树为二叉搜索树。


#### Solution

Language: ****

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
    int sum = 0;
    void traverse(TreeNode* root){
        if(root == nullptr)
            return ;

        traverse(root->right);
        sum += root->val;
        root->val = sum;
        traverse(root->left);
    }

    TreeNode* convertBST(TreeNode* root) {
        traverse(root);
        return root;
    }
};
​
```

## Summary:
首先，BST 的特性大家应该都很熟悉了：

1、对于 BST 的每一个节点 node，左子树节点的值都比 node 的值要小，右子树节点的值都比 node 的值大。

2、对于 BST 的每一个节点 node，它的左侧子树和右侧子树都是 BST。

二叉搜索树并不算复杂，但我觉得它可以算是数据结构领域的半壁江山，直接基于 BST 的数据结构有 AVL 树，红黑树等等，拥有了自平衡性质，可以提供 logN 级别的增删查改效率；还有 B+ 树，线段树等结构都是基于 BST 的思想来设计的。

从做算法题的角度来看 BST，除了它的定义，还有一个重要的性质：BST 的中序遍历结果是有序的（升序）。

这道题就解决了，核心还是 BST 的中序遍历特性，只不过我们修改了递归顺序，降序遍历 BST 的元素值，从而契合题目累加树的要求。

简单总结下吧，BST 相关的问题，要么利用 BST 左小右大的特性提升算法效率，要么利用中序遍历的特性满足题目的要求，也就这么些事儿吧。
