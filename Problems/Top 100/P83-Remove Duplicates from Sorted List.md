# [83\. 删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)


## Description:
Difficulty: **Easy**


给定一个已排序的链表的头 `head` ， _删除所有重复的元素，使每个元素只出现一次_ 。返回 _已排序的链表_ 。

**示例 1：**

![](https://assets.leetcode.com/uploads/2021/01/04/list1.jpg)

```
输入：head = [1,1,2]
输出：[1,2]
```

**示例 2：**

![](https://assets.leetcode.com/uploads/2021/01/04/list2.jpg)

```
输入：head = [1,1,2,3,3]
输出：[1,2,3]
```

**提示：**

*   链表中节点数目在范围 `[0, 300]` 内
*   `-100 <= Node.val <= 100`
*   题目数据保证链表已经按升序 **排列**


## Solutions:

Language: **C++**

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* deleteDuplicates(ListNode* head) {
        //1. 临界条件
        if(head == nullptr)
            return head;
        //2. 变量初始化
        ListNode* left = head;
        ListNode* right = head;
        //3. 循环
        while(right != nullptr){
            if(right->val != left->val){
                left = left->next;
                left->val = right->val;
            }else{
                right = right->next;
            }
        }
        
        left->next = nullptr;
```

## Summary:
