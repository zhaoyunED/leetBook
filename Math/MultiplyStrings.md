#MultiplyStrings
Given two numbers represented as strings, return multiplication of the numbers as a string.

Note: The numbers can be arbitrarily large and are non-negative.



---



```
思路：
按照传统的乘法方法 从string末尾 开始算

string multiply(string num1, string num2)
{
        string sum(num1.size() + num2.size(), '0');

        for (int i = num1.size() - 1; 0 <= i; --i) {
            int carry =0;
            for(int j=num2.size()-1 ; 0<=j ; j--)
            {
                int temp = sum[i+j+1]-'0' + (num1[i]-'0')*(num2[j]-'0')+carry;
                sum[i+j+1] = temp%10+'0';
                carry = temp/10;
            }
            sum[i] += carry; //
        }

        size_t startpos = sum.find_first_not_of("0");
        if (string::npos != startpos) {
            return sum.substr(startpos);
        }
        return "0";
}
```