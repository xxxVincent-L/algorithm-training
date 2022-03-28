### [2\. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)
##Discription:
Difficulty: **Medium**


给你两个 **非空** 的链表，表示两个非负的整数。它们每位数字都是按照 **逆序** 的方式存储的，并且每个节点只能存储 **一位** 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

**示例 1：**

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg)

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

**示例 2：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

**示例 3：**

```
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

**提示：**

*   每个链表中的节点数在范围 `[1, 100]` 内
*   `0 <= Node.val <= 9`
*   题目数据保证列表表示的数字不含前导零


## Solutions:

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
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        
            ListNode *head = new ListNode(0);
            ListNode *res = head;
            int t = 0;
        for(int i = 0; l1 !=nullptr || l2 != nullptr; i++){
            if(l1 != nullptr) t += l1->val, l1 = l1->next;
            if(l2 != nullptr)  t += l2->val, l2 = l2->next;
            
            res->next = new ListNode(t%10);
            res = res->next;
​
            t /= 10;
    }
        if(t > 0){
            res-> next = new ListNode(1);
            res = res->next;
        }
   }

        return head->next;
    }
};
```

##Summary:
* 这道题有点类似于**大数加法**的感觉，所以直接采用相关模板，并进行一定调整即可。
* [对链表的理解](../../Summary/Linked%20List.md)
  * 特指本题结点的创建！当然本文档的代码没有提到这个部分，详见 [leetcode-2](https://leetcode.com/problems/add-two-numbers/submissions/).

