#Number of Digit One
Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

For example:
Given n = 13,
Return 6, because digit 1 occurred in the following numbers: 1, 10, 11, 12, 13.


---


```
思路：编程之美上的题目


对于每一位上能出现的1次数进行统计
比如说：10312
十位1出现1的次数即为103*10加上3(10310, 10311,10312)

百位3出现1的次数为：(10+1)*100

千位0 出现1的次数为：（1*1000）

每一位根据0,1和大于1 分成不同的情况 个有着不同的计算出现1次数方式

int countDigitOne(int n)
{
        long long res =0;
        if(n<=0) return res;
        
        long long fact =1;
        long long low=0;
        long long curr=0;
        long long high=0;
        
        while(n/fact !=0)
        {
            low = n- (n/fact)*fact;
            curr = (n/fact)%10;
            high = n/(fact*10);
            
            switch(curr)
            {
                case 0 : res += high*fact;  break;
                case 1: res+= high*fact +low+1; break;
                default : 
                    res += (high+1)*fact;
            }
            fact = fact *10;
        }
        return res;
}
```