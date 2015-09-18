#PlusOne
Given a non-negative number represented as an array of digits, plus one to the number.

The digits are stored such that the most significant digit is at the head of the list.


---




```
思路：
从末尾判断每个数字加1后是否有进位
不是则跳出返回

vector<int> plusOne(vector<int>& digits) {
        bool carry =true;
        for(int i=digits.size()-1; i>=0 && carry; i--)
        {
            carry = (++digits[i]%10 == 0) ;
            digits[i] %= 10;
        }
            
        if(carry) {
            digits[0]=1;
            digits.push_back(0);
        }

        return digits;
}
```