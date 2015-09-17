#CountPrimes
Description:

Count the number of prime numbers less than a non-negative number, n.

---



思路：
埃拉托色尼选筛法(Sieve of Eratosthenes)

```
int countPrimes(int n)
{
      vector<bool> isPrime(n,true);
        
      for(int i=2;i*i<n;i++)
        {
            if(!isPrime[i]) continue;
            for(int j=i*i ;j<n ;j +=i)
                isPrime[j] = false;
      }
        
     int count =0;//统计数目
     for(int i=2;i<n;i++)
        if(isPrime[i])
          count++;
            
     return count;
}
```