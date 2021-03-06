#Triangle
Given a triangle, find the minimum path sum from top to bottom. 
Each step you may move to adjacent numbers on the row below.

For example, given the following triangle
```[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:
Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

---




```
典型的DP题目 同时只需要 O(n)的空间复杂度
自底向上解决代码简练

int minimumTotal(vector<vector<int> > &triangle) {
    int n = triangle.size();
    vector<int> minlen(triangle.back());
    for (int layer = n-2; layer >= 0; layer--) 
    {
        for (int i = 0; i <= layer; i++) //每一行有layer个元素
        {
            minlen[i] = min(minlen[i], minlen[i+1]) + triangle[layer][i]; 
        }
    }
    return minlen[0];
}
```
