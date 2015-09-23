#Power of Two
Given an integer, write a function to determine if it is a power of two.

```
思路：

bool isPowerOfTwo(int n)
{
        if(n == INT_MIN)
            return false;
        int res=0;
        while(n)
        {
            n = n&(n-1);
            res++;
        }
        
        return res == 1;
}
```