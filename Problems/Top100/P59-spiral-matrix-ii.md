### [59\. 螺旋矩阵 II](https://leetcode-cn.com/problems/spiral-matrix-ii/)

Difficulty: **给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。   示例 1： 输入：n = 3 输出：[[1,2,3],[8,9,4],[7,6,5]] 示例 2： 输入：n = 1 输出：[[1]]   提示： 1 <= n <= 20 **


给你一个正整数 `n` ，生成一个包含 `1` 到 `n<sup>2</sup>` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。

**示例 1：**

![](https://assets.leetcode.com/uploads/2020/11/13/spiraln.jpg)

```
输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]
```

**示例 2：**

```
输入：n = 1
输出：[[1]]
```

**提示：**

*   `1 <= n <= 20`


#### Solution

Language: ****

```c++
class Solution
{
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix)
    {
        if (matrix.empty()) return {};
        vector<int> res;
        int l = 0;                      //左边界
        int r = matrix[0].size() - 1;   //右边界
        int t = 0;                      //上边界
        int b = matrix.size() - 1;      //下边界
        while (true)
        {
            //left -> right
            for (int i = l; i <= r; i++) res.push_back(matrix[t][i]);
            if (++t > b) break;
            //top -> bottom
            for (int i = t; i <= b; i++) res.push_back(matrix[i][r]);
            if (--r < l) break;
            //right -> left
            for (int i = r; i >= l; i--) res.push_back(matrix[b][i]);
            if (--b < t) break;
            //bottom -> top
            for (int i = b; i >= t; i--) res.push_back(matrix[i][l]);
            if (++l > r) break;
        }
        return res;
    }
};
​
```
