#Numberof1Bits
Write a function that takes an unsigned integer and returns the number of 
'1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer '11' has binary representation 00000000000000000000000000001011, 
so the function should return 3.



---

思路：

这是老题目了,n&(n-1) 是将最低位的为1的位变成0

```
int hammingWeight(uint32_t n)
{
        int res=0;
        while(n)
        {
            n = n&(n-1);
            res++;
        }
        return res;
}
```