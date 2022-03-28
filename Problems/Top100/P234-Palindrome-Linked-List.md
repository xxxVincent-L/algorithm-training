# [234\. 回文链表](https://leetcode-cn.com/problems/palindrome-linked-list/)

## Descriptions:

Difficulty: **Easy**


给你一个单链表的头节点 `head` ，请你判断该链表是否为回文链表。如果是，返回 `true` ；否则，返回 `false` 。

**示例 1：**

![](https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg)

```
输入：head = [1,2,2,1]
输出：true
```

**示例 2：**

![](https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg)

```
输入：head = [1,2]
输出：false
```

**提示：**

*   链表中节点数目在范围`[1, 10<sup>5</sup>]` 内
*   `0 <= Node.val <= 9`

**进阶：**你能否用 `O(n)` 时间复杂度和 `O(1)` 空间复杂度解决此题？


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
    bool isPalindrome(ListNode* head) {
            vector<int> res;
        ListNode* temp = head;
​
        while(temp!=nullptr){
​
            res.push_back(temp->val);
            temp = temp->next;
        }
        for(int i = 0, j = res.size()-1; i <=j; i++,j--){
            if(res[i]!=res[j])
                return false;
        }
        return true;
    }
};
```

## Summary:
