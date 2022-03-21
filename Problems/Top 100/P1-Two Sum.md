# [1\. 两数之和](https://leetcode-cn.com/problems/two-sum/)

## Description：
Difficulty: **Easy**




给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** _`target`_  的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

**提示：**

*   `2 <= nums.length <= 10<sup>4</sup>`
*   `-10<sup>9</sup> <= nums[i] <= 10<sup>9</sup>`
*   `-10<sup>9</sup> <= target <= 10<sup>9</sup>`
*   **只会存在一个有效答案**

**进阶：**
你可以想出一个时间复杂度小于 `O(n<sup>2</sup>)` 的算法吗？


## Solutions：

Language: **C++**

* Sol 1

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        //1. 初始化->变量定义
        int i,j;

        //2.循环
        for(i=0;i<nums.size()-1;i++)
        {
            for(j=i+1;j<nums.size();j++)
            {
                if(nums[i]+nums[j]==target)
                {
                   return {i,j};
                }
            }
        }
        return {i,j};
    };
};
```

* Sol 2
```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        //1. 初始化->变量定义
        unordered_map<int, int> map;
        //2.循环
        for(int i = 0; i< nums.size(); i++){
            
            auto it = map.find(target - nums[i]);
            if(it != map.end()){
                return {it->second, i};
            }
            map[nums[i]] = i;
        }
        return {};
    }
};
```

## Summary:

* Sol1:这个解法就很质朴了。利用两层循环+判断语句进行处理。
  * 时间复杂度为**O(n^2)**,略高且不出彩。
* Sol2:这个解法相对巧妙很多，主要在于利用稍复杂的数据结构unordered_map.
  * 时间复杂度为**O(n)**，减少了很多。
  >相比普通的map在增删查改的时间复杂度上有显著的提升。unordered_map的搜索时间复杂度是O(1).
