# [4\. 寻找两个正序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

## Description:
Difficulty: **Hard**


给定两个大小分别为 `m` 和 `n` 的正序（从小到大）数组 `nums1` 和 `nums2`。请你找出并返回这两个正序数组的 **中位数** 。

算法的时间复杂度应该为 `O(log (m+n))` 。

**示例 1：**

```
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```

**示例 2：**

```
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```

**提示：**

*   `nums1.length == m`
*   `nums2.length == n`
*   `0 <= m <= 1000`
*   `0 <= n <= 1000`
*   `1 <= m + n <= 2000`
*   `-10<sup>6</sup> <= nums1[i], nums2[i] <= 10<sup>6</sup>`


## Solutions:

Language: **C++**

```c++
class Solution {
public:
  
    double findMedianSortedArrays(vector<int>& nums1, vector<int>&nums2){
        int len = nums1.size() + nums2.size();
        
        double res = 0;
        
        if(len % 2 == 1){
            res = getKthElement(len/2+1,nums1,nums2);
            // cout<<res<<"+";
            return res;
        }else{
            int temp1 = getKthElement(len/2+1,nums1,nums2);
            int temp2 = getKthElement(len/2 ,nums1,nums2);
            res = ( temp1+temp2 )/2.0 ;
            // cout<<res<<"-"<<temp1<<"-"<<temp2;
            return res;  
        }
    }
    
    int getKthElement(int k, vector<int>& nums1, vector<int>& nums2){
        int len1 = nums1.size();
        int len2 = nums2.size();
        int index1 = 0, index2 = 0;
        
        while(1){
            if(len1 == index1){
                return nums2[index2 + k -1];
            }
            if(len2 == index2){
                return nums1[index1 + k -1];
            }
            if( k == 1){
                return min(nums1[index1], nums2[index2]);
            }

            int half = k/2;
            int newIndex1 = min(half+index1,len1) -1;
            int newIndex2 = min(half+index2,len2) -1;
            if(nums1[newIndex1] <= nums2[newIndex2]){
                k -= newIndex1 - index1 +1;
                index1 = newIndex1 + 1;
            }else{
                k -= newIndex2 - index2 +1;
                index2 = newIndex2 + 1;
            }

        }

    }


};
```

## Summary:
