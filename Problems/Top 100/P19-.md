# [19\. 删除链表的倒数第 N 个结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)
## Description:
Difficulty: **Medium**


给你一个链表，删除链表的倒数第 `n`个结点，并且返回链表的头结点。

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg)

```
输入：head = [1,2,3,4,5], n = 2
输出：[1,2,3,5]
```

**示例 2：**

```
输入：head = [1], n = 1
输出：[]
```

**示例 3：**

```
输入：head = [1,2], n = 1
输出：[1]
```

**提示：**

*   链表中结点的数目为 `sz`
*   `1 <= sz <= 30`
*   `0 <= Node.val <= 100`
*   `1 <= n <= sz`

**进阶：**你能尝试使用一趟扫描实现吗？


## Solution

Language: **C++**

```c++
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
    
    //1.抽象出一个函数来了！
    ListNode* findFromEnd(ListNode* head, int n){
            ListNode* p = head;
        ListNode* q = head;
        for(int i = 0; i< n ;i++){
            // if(p == nullptr)
            //     break;
            p = p->next;
        }
        while(p != nullptr){
            p = p->next;
            q = q->next;
        }
        return q;
    }
    
    ListNode* removeNthFromEnd(ListNode* head, int n){    
```
## Summary:
