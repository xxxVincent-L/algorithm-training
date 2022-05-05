# [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

## Descriptions:
Difficulty: **Easy**


一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

**示例 1:**

```
输入: [0,1,3]
输出: 2
```

**示例 2:**

```
输入: [0,1,2,3,4,5,6,7,9]
输出: 8
```

**限制：**

`1 <= 数组长度 <= 10000`


## Solutions:

Language: **C++**

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int i = 0, j = nums.size()-1;

        while(i <= j){
            int x = i + (j-i)/2;
            if(nums[x] == x)  i = x+1;
            else j = x-1;
        }
        return i;
    }
};
​
```

## Summary:
https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/solution/mian-shi-ti-53-ii-0n-1zhong-que-shi-de-shu-zi-er-f/
