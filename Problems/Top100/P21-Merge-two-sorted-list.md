# [21\. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

## Descriptions：

Difficulty: **Easy**


将两个升序链表合并为一个新的 **升序** 链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg)

```
输入：l1 = [1,2,4], l2 = [1,3,4]
输出：[1,1,2,3,4,4]
```

**示例 2：**

```
输入：l1 = [], l2 = []
输出：[]
```

**示例 3：**

```
输入：l1 = [], l2 = [0]
输出：[0]
```

**提示：**

*   两个链表的节点数目范围是 `[0, 50]`
*   `-100 <= Node.val <= 100`
*   `l1` 和 `l2` 均按 **非递减顺序** 排列


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
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        ListNode* res = new ListNode(-1);
        ListNode* head = res;
        ListNode* p1 = list1;
        ListNode* p2 = list2;
        
        while(p1 != nullptr && p2 != nullptr){
             if (p1->val <= p2->val){
                // 笑死 head确定下一个 然后竟然不更新是吧
            head->next = p1;
            head = head->next;
            p1 = p1->next;
            cout<<head->val<<endl;
​
        }
        else{
            head->next = p2;
            head = head->next;
​
            p2 = p2->next;
        }
​
        }
      
            if(p1 == nullptr){
​
                head->next = p2;
            }
            if(p2 == nullptr){
​
                head->next = p1;
            }
        return res->next;
    }
};
```

## Summary:
  这个就与归并排序类似了！
  利用双指针的技巧将两个链表上各自的结点拼接到一个新的链表！

  ### 时间复杂度\空间复杂度：
  * 时间复杂度： **O(n)**
   遍历到两个链表
  * 空间复杂度： **O(n)**
