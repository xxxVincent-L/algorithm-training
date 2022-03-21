# [3\. 无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)


## Descriptions:
Difficulty: **Medium**


给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串**的长度。

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**提示：**

*   `0 <= s.length <= 5 * 10<sup>4</sup>`
*   `s` 由英文字母、数字、符号和空格组成


## Solutions:

Language: **C++**

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
      //1. 变量确定！
        unordered_map<char,int> window;
        int left = 0, right =0;
        int res = 0;
        
        //2.外层循环 确定右边界
        while(right < s.size()){
            char tempRight = s[right++];
            window[tempRight]++;
            //3.内存循环 确定左边界
            while(window[tempRight] > 1){
                char tempLeft = s[left++];
                window[tempLeft]--;
            }
            //4.保存每次结果！
            res = max(res, right -left);
        }
        return res;
    }
};
```
## Summary:
