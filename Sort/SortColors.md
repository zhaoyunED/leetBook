#SortColors
Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, 
with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note:
You are not suppose to use the library's sort function for this problem.

click to show follow up.

Follow up:
A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, 
then 1's and followed by 2's.

Could you come up with an one-pass algorithm using only constant space?


---


```
方法1： 计数排序，需要遍历两遍数组

void sortColors(vector<int>& nums) {
        int numOne=0;
        int numZero=0;
        
        for(auto num : nums)
        {
            if(0 == num)
                numZero++;
            else if(1 ==num)
                numOne++;
        }
        
        for(int i=0;i<nums.size();i++)
        {
            if(i+1 <=numZero)
                nums[i]=0;
            else if(i+1 <=(numZero+numOne))
                nums[i] =1;
            else nums[i] =2;
        }
}


方法2 :类似 two pointers 只需要遍历一遍数组

void sortColors(vector<int>& nums) {
        int n =nums.size();
        
        int i=-1, j=-1;//分别是0,1 的索引

        for(int p = 0; p < n; p++) {
    
           int v = A[p];
           A[p] = 2;
    
           if (v == 0) {
    
              A[++j] = 1;
              A[++i] = 0;
           }
           else if (v == 1) {
    
               A[++j] = 1;
           }
        }
    }


方法3
void sortColors(int A[], int n) {
    int j = 0, k = n-1;//分别表示下一个 0和1应该出现的位置
    for (int i=0; i <= k; i++) {
        if (A[i] == 0)
            swap(A[i], A[j++]);
        else if (A[i] == 2)
            swap(A[i--], A[k--]);
    }
}
```