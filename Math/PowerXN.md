#Power(x,n)
Implement pow(x, n).
---



``` 
思路:
利用的是 蒙哥马利快速模乘算法 
将幂转换为二进制
注意INT_MIN的绝对值比INT_Max大1，因此nINT_MIN转换为正数求幂时，为要多乘以一个x

double myPow(double x, int n) {

	if(n<0)
	 {
		if(n == INT_MIN)
			return 1.0/(myPow(x,INT_MAX))*x;
		else
			return 1.0/myPow(x,-n);
	 }

	 if(n==0)
		 return 1.0;

	 double result =1.0;
	 double ass =x;

	 for( ;n>0;n >>= 1)
	 {
		if(n & 0x1)
			result *=ass;
		ass *=ass;
	 }
	 return result;
 }
 ```
