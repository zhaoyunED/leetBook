#FactorialTrailingZeroes
Given an integer n, return the number of trailing zeroes in n!.


---



```
思路：
又是一道编程之美上的题目
n的阶乘 末尾能造成出现0 只有可能2*5形成.
也就是变成了1...n之间的数 有多少个2的因子和5因子

而其中出现5因子的次数是远远少于2的，因此最终问题就变成了求
1...n中含有多少个5因子（像25这样的数是提供2个5因子）

int trailingZeroes(int n)
{
        if(n<=0) return 0;
        int ret=0;
        while(n)
        {
            ret += n/5;
            n= n/5;
        }
        return ret;
}
```