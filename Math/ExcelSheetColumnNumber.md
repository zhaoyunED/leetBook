#ExcelSheetColumnTitle
Related to question Excel Sheet Column Title

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28 


---



```
思路:
相当于一个26进制数
int titleToNumber(string s)
{
        int res=0;
        for(auto ss :s)
        {
            res = res*26 + ss-'A'+1;
        }
        return res;
}
```