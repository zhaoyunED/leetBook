#ValidParentheses
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.



```
思路： 这个题目很简单，用一个栈来保存 "左边"类型的括号
bool isValid(string s)
{
        stack <char> stk;
        for(char& c: s)
        {
            switch(c)
            {
                case '(':
                case '[':
                case '{': stk.push(c);break;
                case ')': if(stk.empty()|| stk.top() != '(') return false; else stk.pop(); break;
                case ']': if(stk.empty() || stk.top() != '[' )return false; else stk.pop(); break;
                case '}': if(stk.empty() || stk.top() != '{' )return false; else stk.pop(); break;
                default : ;
            }
        }
        
        return stk.empty();
}
```