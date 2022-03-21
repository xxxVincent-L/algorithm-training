# [23\. 合并K个升序链表](https://leetcode-cn.com/problems/merge-k-sorted-lists/)

##Descriptions:

Difficulty: **Hard**


给你一个链表数组，每个链表都已经按升序排列。

请你将所有链表合并到一个升序链表中，返回合并后的链表。

**示例 1：**

```
输入：lists = [[1,4,5],[1,3,4],[2,6]]
输出：[1,1,2,3,4,4,5,6]
解释：链表数组如下：
[
  1->4->5,
  1->3->4,
  2->6
]
将它们合并到一个有序链表中得到。
1->1->2->3->4->4->5->6
```

**示例 2：**

```
输入：lists = []
输出：[]
```

**示例 3：**

```
输入：lists = [[]]
输出：[]
```

**提示：**

*   `k == lists.length`
*   `0 <= k <= 10^4`
*   `0 <= lists[i].length <= 500`
*   `-10^4 <= lists[i][j] <= 10^4`
*   `lists[i]` 按 **升序** 排列
*   `lists[i].length` 的总和不超过 `10^4`


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
    ListNode* mergeKLists(vector<ListNode*>& lists) {      
​
        //1. 变量定义
        ListNode* res = new ListNode(-1);
        ListNode* head = res;
        
        // 这题里最重要的就是小根堆的定义！
        // priority_queue<ListNode*, vector<ListNode*>, greater<ListNode*->val>> heap;
        // priority_queue<int, vector<int>, greater<int>> heap;
        
        // 比较函数！
        struct cmp {
            bool operator() (ListNode* a, ListNode* b) {
                return a->val > b->val;
            }
        };
  
        priority_queue<ListNode*, vector<ListNode*>, cmp> heap;
​
        
        for(auto list:lists){
            if(list != nullptr)
                heap.push(list);
​
        }
        
        while(!heap.empty()){
            ListNode* temp = heap.top();

            heap.pop();
​
            head->next = temp;
            if(temp->next!=nullptr){
                heap.push(temp->next);
                // cout<<temp->next->val<<"*"<<endl;
            }
            
            head = head->next;
        }
        return res->next;
    }
};
```

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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        struct cmp {
            bool operator() (ListNode* a, ListNode* b) {
                return a->val > b->val;
            }
        };
        auto dummy = new ListNode(-1), cur = dummy;
        priority_queue<ListNode*, vector<ListNode*>, cmp> heap;
        for (auto l : lists) {
            if (l) heap.push(l);
        }
        while (heap.size()) {
            auto t = heap.top();
            heap.pop();
            cur = cur->next = t;
            if (t->next) heap.push(t->next);
        }
        return dummy->next;
    }
};
```

## Summary:


## Inference:
* [Docs1-Heap](https://xiaoneng.blog.csdn.net/article/details/103206628?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ETopBlog-1.topblog&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ETopBlog-1.topblog&utm_relevant_index=2)
* [Docs2-Heap](https://blog.csdn.net/largecub233/article/details/73321440)
