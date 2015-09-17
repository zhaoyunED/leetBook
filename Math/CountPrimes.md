#CountPrimes
Description:

Count the number of prime numbers less than a non-negative number, n.

---



思路：
埃拉托色尼选筛法(Sieve of Eratosthenes)


```
用一个大小为n的表来记录每个数的素数性

对于每个质数n，其2*n,3*n,4*n 就都不是质数
遍历每个数，判断一个数若是质数，那就把其所有的的倍数的值设置为false.

最后统计素数的数目即可

int countPrimes(int n)
{
      vector<bool> isPrime(n,true);
        
      for(int i=2;i*i<n;i++)
        {
            if(!isPrime[i]) continue;
            for(int j=i*i ;j<n ;j +=i)//j 从i*i开始即可
                isPrime[j] = false;
      }
        
     int count =0;//统计数目
     for(int i=2;i<n;i++)
        if(isPrime[i])
          count++;
            
     return count;
}
```