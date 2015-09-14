#RegularExpressionMatching
Implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
```
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

---


方法1：递归方法
```
bool isMatch(string s, string p) 
{
        if ( p.empty() ) return s.empty();
        // p's next is not *
        if ( p[1]!='*' )
        {
            return ( s[0]==p[0] || (p[0]=='.' && !s.empty()) ) && Solution::isMatch(s.substr(1), p.substr(1));
        }
        // p's next is * and curr s match curr p
        int i = 0;
        for ( ; s[i]==p[0] || (p[0]=='.' && i<s.size()); ++i)
        {
            if ( Solution::isMatch(s.substr(i), p.substr(2)) ) return true; 
        }
        // p's next is * but curr s not match curr p
        return Solution::isMatch(s.substr(i), p.substr(2));
}
```








方法2：动态规划
```
bool isMatch(string s, string p) {
        
        int m = s.size(), n = p.size();
        vector<vector<bool>> f(m + 1, vector<bool>(n + 1, false));

        f[0][0] = true;
        for (int i = 1; i <= m; i++)
            f[i][0] = false;
        // p[0.., j - 3, j - 2, j - 1] matches empty iff p[j - 1] is '*' and p[0..j - 3] matches empty
        for (int j = 1; j <= n; j++)
            f[0][j] = j > 1 && '*' == p[j - 1] && f[0][j - 2];

        for (int i = 1; i <= m; i++)
            for (int j = 1; j <= n; j++)
                if (p[j - 1] != '*')
                    f[i][j] = f[i - 1][j - 1] && (s[i - 1] == p[j - 1] || '.' == p[j - 1]);
                else
                    // p[0] cannot be '*' so no need to check "j > 1" here
                    f[i][j] = f[i][j - 2] || (s[i - 1] == p[j - 2] || '.' == p[j - 2]) && f[i - 1][j];

        return f[m][n];
}
```

此题详细分析可参考：
