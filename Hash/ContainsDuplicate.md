#ContainsDuplicate
Given an array of integers, find if the array contains any duplicates. 
Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.



---


```
方法1：
bool containsDuplicate(vector<int>& nums) {
        return nums.size() > set<int>(nums.begin(), nums.end()).size();        
    }

方法2：
bool containsDuplicate(vector<int>& nums) 
{
        int size=nums.size();
        sort(nums.begin(),nums.end());
        nums.erase(unique(nums.begin(),nums.end()),nums.end());
        return (size!=nums.size());
}

上述两个方法都是利用了STL里面的方法，常规方法用hashmap来保存每一个数是否出现过也是可以的
```