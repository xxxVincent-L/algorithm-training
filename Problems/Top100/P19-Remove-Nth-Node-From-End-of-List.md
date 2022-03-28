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

**进阶:** 你能尝试使用一趟扫描实现吗？


## Solution

Language: **C++**

```c++

/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
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
            //     break;
            p = p->next;
        }
        while(p != nullptr){
            p = p->next;
            q = q->next;
        }
        return q;
    }

    ListNode* removeNthFromEnd(ListNode* head, int n){
        if(head == nullptr || head->next== nullptr)
            return {};

        ListNode* temp = new ListNode(-1);
        temp->next = head;

        ListNode* q = findFromEnd(temp,n+1);

        // if(q->next !=nullptr)
        q ->next = q->next->next;
        return temp->next;
    }
};  
```
## Summary:
本题主要应用双指针进行处理！
解题过程分成两个阶段：

* 找出倒数第K个数
  假设共有**N**个数，那么倒数第K个数也即正数的第**N-K**个数。且知链表无法直接知道N，且单链表无法直接反转。
    * p指针先走k步
    * 此后q指针和p指针同时开始走！直到p指针到nullptr。
* 删除某个数
  * **问题**：
    这里有点坑在于——**如果找到倒数第K个结点，你很难通过常规手段删除（因为你无法回溯到上个结点）**，所以我们采用找到倒数**K+1**个结点，然后进行删除操作。那么这样一来在删除倒数第**N**个结点，也即第一个结点时，会报错，因为我们并不存在第**0**个结点。
  * **解决方法**：
    新建一个结点，并使其next指针指向第一个结点！
