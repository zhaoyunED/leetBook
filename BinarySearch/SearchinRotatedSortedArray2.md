#SearchinRotatedSortedArray2
Follow up for "Search in Rotated Sorted Array":
What if duplicates are allowed?

Would this affect the run-time complexity? How and why?

Write a function to determine if a given target is in the array.


---



```
思路：
基本思路是和SearchinRotatedSortedArray一致的。但是允许重复元素出现后该算法的最差时间复杂度变为了O(n)

考虑 11111113 rotate之后 变为  11311111
此时 A[m] == A[l] == A[h] 无法判断要查找的target落在哪个区域内因此只能



bool search(vector<int>& A, int key) {
        
        int l = 0, r = A.size()-1;
        
        while (l <= r) {
            int m = l + (r - l)/2;
            if (A[m] == key) return true; //return m
            if (A[l] < A[m]) { //左边是排好序的
                if (A[l] <= key && key < A[m])
                    r = m - 1;
                else
                    l = m + 1;
            } else if (A[l] > A[m]) { //右边是排好序的
                if (A[m] < key && key <= A[r])
                    l = m + 1;
                else
                    r = m - 1;
            } else if(A[m] != A[r])
            {
                l=m+1;
            }else 
                l++;
        }
        return false;
}


```