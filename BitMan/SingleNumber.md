#SingleNumber
Given an array of integers, every element appears twice except for one. Find that single one.

Note:
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?


---


```
思路：将数组里面的元素异或一遍 相同的两个数会异或为0，只留下出现一次的那个数

int singleNumber(int A[], int n)
{
        for (int i = 1; i < n; ++i)
                A[0] ^= A[i];
             return A[0];
}
```