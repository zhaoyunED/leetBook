
Given an unsorted integer array, find the first missing positive integer.

For example,
Given [1,2,0] return 3,
and [3,4,-1,1] return 2.

Your algorithm should run in O(n) time and uses constant space.




---


思路：

每次把数组的元素移动到其对应的位置之后从头遍历找不符合条件的
index(此题目在面试中遇到过)

移动的元素大小需要在[0,nums.size()]之间，大小不在这范围内的直接跳过即可。

```
int firstMissingPositive(vector<int>& nums)
{
        int n = nums.size();
        for(int i=0;i<n;i++)
        {
            while(nums[i]>0 && nums[i]<=n && nums[i] != nums[nums[i]-1])
                swap(nums[i],nums[nums[i]-1]);
        }
        for(int i=0;i<n;i++)
            if(nums[i]!=i+1)
                return i+1;
        return n+1;
}```
