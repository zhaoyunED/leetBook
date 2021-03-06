#SearchinRotatedSortedArray
Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

You are given a target value to search. If found in the array return its index, otherwise return -1.

You may assume no duplicate exists in the array.


---


```
方法1: 
int search(vector<int>& nums, int target) 
{
        int lo = 0;
        int hi = nums.size() - 1;
        while (lo < hi) { //基本也是 二分查找 但是要加特殊的判断 画个图 就比较容易理解
            int mid =lo+(hi-lo)/2;
            if (nums[mid] == target) return mid;
    
            if (nums[lo] <= nums[mid]) { //因为rotatded了 所以不一定哪个大
                if (target >= nums[lo] && target < nums[mid]) {
                    hi = mid - 1;
                } else {
                    lo = mid + 1;
                }
            } else {
                if (target > nums[mid] && target <= nums[hi]) {
                    lo = mid + 1;
                } else {
                    hi = mid - 1;
                }
            }
        }
        return nums[lo] == target ? lo : -1;
}

方法2
先找到旋转后数组中元素最小的值的下标low，这样数组旋转(移动)的距离就是low

之后用传统的二分查找来查询元素target，每次通过
            mid=lo+(hi-lo)/2;
            realmid=(mid+rot)%nums.size();
找到实际的realmid来进行二分

int search(vector<int>& nums, int target) 
{
        int lo=0,hi=nums.size()-1;
       
        while(lo<hi){
            int mid=lo+(hi-lo)/2;
            if(nums[mid]>nums[hi]) lo=mid+1;
            else hi=mid;
        }//先找到拐点，然后再用传统的二分查找方法
        
        int rot=lo;
        lo=0;hi=nums.size()-1;
        
        while(lo<=hi){
            int mid=lo+(hi-lo)/2;
            int realmid=(mid+rot)%nums.size();
            if(nums[realmid]==target)return realmid;
            if(nums[realmid]<target)lo=mid+1;
            else hi=mid-1;
        }
        return -1;
}
```