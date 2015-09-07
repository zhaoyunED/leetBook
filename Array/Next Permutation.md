#NextPermutation
Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place, do not allocate extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

1,2,3 → 1,3,2

3,2,1 → 1,2,3

1,1,5 → 1,5,1



---

思路：

对于一个序列，从右向左找第一个升序的数字，其下标为pivot

* 
若pivot>0
下一步我们就需要找到(从右向左找)第一个比nums[pivot-1]大的元素，假设其下表为large,交换nums[pivot-1]与nums[large],最后我们将序列下标从pivot到末尾的元素reverse

* 
若pivot<=0 整个序列则是降序排列，该序列的下一个序列需要将整个现有序列reverse


举个例子可能会更容易理解

序列：
4 6 5 3 2 1 找到pivot元素为6

从末尾找第一个比4大的元素为5，交换这两个元素，为

5 6 4 

```
void nextPermutation(vector<int>& nums) 
{
        int end = nums.size()-1;
        int pivot = end;
        while(pivot>0)
        {
            if(nums[pivot] > nums[pivot-1] )  //从后找第一个升序的数字
                break;
            pivot--;
        }
        
        if(pivot>0)
        {
            pivot--;
            int large = end;
            //找到第一个比nums[pivot]大的数
            while(nums[large] <= nums[pivot]) large--;  
            swap(nums[large],nums[pivot]);
            reverse(nums.begin()+pivot+1,nums.end());
        }else
        {
            reverse(nums.begin(),nums.end());
        }
}
```