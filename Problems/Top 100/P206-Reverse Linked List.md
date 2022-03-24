# [206\. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)

## Descriptions:
Difficulty: **Easy**

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。


**示例 1：**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

```
输入：head = [1,2,3,4,5]
输出：[5,4,3,2,1]
```

**示例 2：**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

```
输入：head = [1,2]
输出：[2,1]
```

**示例 3：**

```
输入：head = []
输出：[]
```

**提示：**

*   链表中节点的数目范围是 `[0, 5000]`
*   `-5000 <= Node.val <= 5000`

**进阶：**链表可以选用迭代或递归方式完成反转。你能否用两种方法解决这道题？


## Solutions:

Language: **C++**

### 递归:
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
    ListNode* reverseList(ListNode* head) {
        if(head == nullptr || head->next == nullptr)
            return head;
        
        ListNode* temp = reverseList(head->next);
        
        head->next->next = head;
        head->next=nullptr;
        
        // 返回值没搞定！
        return temp;
    }
};
```

### 迭代：

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
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr;
        ListNode* cur = head;

        while(cur != nullptr){
            ListNode* temp = cur->next;
            cur->next=pre;
            pre = cur;
            cur = temp;
        }
        return pre;
    }
};
```

## Summary:
