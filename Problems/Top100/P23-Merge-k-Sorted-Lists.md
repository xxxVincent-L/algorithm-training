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
* 我觉得和P21对比，其实思路也还是清晰的。无非就是——**从两个数中选出最小值演变到从多个数中选出最小值**
* 那么问题就转变到——**如何以代价最小的方式选到某组数中的最小值！** 那么结合空间复杂度进行考虑，以及本题的特点得出使用**小根堆**。
* **小根堆**的定义方法也在此有待考量！
  > 默认的priority_queue是大根堆

    构造方法：
  * 取反构造小根堆
  * **priority_queue(int, vector\<int>,greater\<int>)**
   这里有一点需要额外注意：greater\<int> 中间比较的数值只能是整型！！！即使是ListNode->val 都不可以！所以还是要使用比较函数
   ```c++
    struct cmp {
       bool operator() (ListNode* a, ListNode* b) {
           return a->val > b->val;
           }
        };
   ```
   > 在这里耗费了很多时间！
* C++中并没有 **poll()** 方法，只得用取**top()**\弹出**pop()** 来组合替代！


## Inference:
* [Docs1-Heap](https://xiaoneng.blog.csdn.net/article/details/103206628?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ETopBlog-1.topblog&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ETopBlog-1.topblog&utm_relevant_index=2)
* [Docs2-Heap](https://blog.csdn.net/largecub233/article/details/73321440)


* [Docs3-Compare Func](https://blog.csdn.net/woxiaohahaa/article/details/53191247)

* [Docs4-Compare Func in STL](https://blog.csdn.net/ivan_zjj/article/details/8654728)
