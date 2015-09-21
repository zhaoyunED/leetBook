#GenerateParenthesis
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:
"((()))", "(()())", "(())()", "()(())", "()()()"


---




```
思路： 递归过程需要记录还需要生成多少个  “（”和 “）”
一开始将")"0设置为0可保证 左括号的数目总是 大于等于右括号的数目 并且 左括号总是先加入字符串

vector<string> generateParenthesis(int n) 
{
        vector<string> res;
        addingpar(res, "", n, 0);
        return res;
}
    
void addingpar(vector<string> &v, string str, int n, int m)
{
        if(n==0 && m==0) {
            v.push_back(str);
            return;
        }
        if(n > 0){ addingpar(v, str+"(", n-1, m+1); }
        if(m > 0){ addingpar(v, str+")", n, m-1); }
        
}
```