#UniquePath
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. 
The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?



---

方法1：
动态规划题目，很简单，空间复杂度O(m*n)
```
int uniquePaths(int m, int n) {
        int f[m][n];  
        memset(f, 0, sizeof(int) * m * n);  
        for (int i = 0; i < m; i++) {  
            f[i][0] = 1;  
        }  
        for (int j = 0; j < n; j++) {  
            f[0][j] = 1;  
        }  
        for (int i = 1; i < m; i++) {  
            for (int j = 1; j < n; j++) {  
                f[i][j] = f[i - 1][j] + f[i][j - 1];  
            }  
        }  
        return f[m - 1][n - 1]; 
}
```

方法2：将空间复杂度降到O(n)
```
int uniquePaths(int m, int n)
{
        if(m ==1 || n==1) return 1;
        
        vector<int> sum(n,1);
        
        for(int i=1; i<m ;i++)
        {
            for(int j=1 ; j<n; j++)
                sum[j] = sum[j-1]+sum[j];
        }
        
        return sum[n-1];
}
```
方法3：排列组合的方法,该题目其实就是计算$$c_{3}^{5}=25$$
```
int uniquePaths(int m, int n)
{
        int A = m + n - 2, B = std::min(m - 1, n - 1);
        long long result = 1;
        for (int i = 1; i <= B; ++i)
            result = result * A-- / i;
        return static_cast<int>(result);
}
```
