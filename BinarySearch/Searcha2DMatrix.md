#Searcha2DMatrix
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
For example,

```
Consider the following matrix:

[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
Given target = 3, return true.
```


---


```
The first integer of each row is greater than the last integer of the previous row 
表明了这个数组其实就是一个排好序的数列，只不过用二维数组的形式表示了出来，所以我们方法一 可以用两次二分查找找到对应元素  或者方法2直接把二维数组当成一个序列来看

方法1 两次二分查找

bool searchMatrix(vector<vector<int> > &matrix, int target) {
        if(matrix.size()<=0 || matrix[0].size()<=0)
            return false;
        int left = 0;  
        int right = matrix.size()-1;
        
        while(left<=right)
        {
            int mid = left+(right-left)/2;
            
            if(matrix[mid][0]>target)
            {
                right = mid-1;
            }else if(matrix[mid][0] < target)
            {
                left = mid+1;
            }else{
                return true;
            }
        }
        
        if(right == -1)
            return false;
        else{
            
            int row = right;  
            int left = 0;  
            int right = matrix[row].size()-1;  
            
            while(left<=right)
            {
                int mid = left+(right-left)/2;
                if(matrix[row][mid]>target)
                {
                    right = mid-1;
                }else if(matrix[row][mid] < target)
                {
                    left = mid+1;
                }else{
                    return true;
                }
            }
            
            return false;
        }
    }


方法2 直接看成一个连贯的array

bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int n = matrix.size();
        int m = matrix[0].size();
        int l = 0, r = m * n - 1;
        while (l <= r){
            int mid = l+((r-l)>>1);
            int row = mid /m;
            int col = mid %m;
            if(matrix[row][col] == target)
                return true;
            else if (matrix[row][col] < target)
                l = mid + 1;
            else 
                r = mid-1;
        }
        return false;
    }
```
