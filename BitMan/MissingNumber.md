#MissingNumber
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

For example,
Given nums = [0, 1, 3] return 2.

Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?


---

```
思路：
可参考题目FirstMissingPositive
对于数组中每个元素 

若是  nums[i]>=n 跳过这个元素
若是  nums[i]<n  并且nums[i] != i 那么将 num[i] swap到第i个位置上， swap来的新元素若还是 ！=i 继续swap 直到nums[i]>=n

最后遍历一遍数组若是 nums[i] != i

int missingNumber(vector<int>& nums) 
{
        
        int n = nums.size();
        for(int i=0;i<n;i++)
        {
            while(nums[i]<n && nums[i] != i)
                swap(nums[i],nums[nums[i]]);
        }
        
        for(int i=0;i<n;i++)
            if(nums[i] != i)
                return i;
        return n;
    }
```