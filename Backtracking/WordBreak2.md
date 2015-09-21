#WordBreak2
Given a string s and a dictionary of words dict, add spaces in s to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

```
For example, given
s = "catsanddog",
dict = ["cat", "cats", "and", "sand", "dog"].

A solution is ["cats and dog", "cat sand dog"].
```


---


``` 
思路：
题目略复杂，但总体上还是DFS+Bk

开始需要记录每个点之前 那些点是可以切割的
用vector<int>[s.size()+1] 来保存
void dfs(vector<string> &result,vector<int> * vect,int end,vector<string> cur,string s)
{
           
            if(end==0)
            {
                string res="";
                for(string ss:cur)
                {
                    if(res != "") res = ss+" "+res;
                    else res = ss;
                }
                result.push_back(res);
                return;
            }
            
             
            
            for(auto idx : vect[end])
            {
                string temp = s.substr(idx,end-idx);
                cur.push_back(temp);
                dfs(result,vect,idx,cur,s);
                cur.pop_back();
            }
}


vector<string> wordBreak(string s, unordered_set<string>& dict)
{
                vector<string> result;
                if(dict.size()==0) return result;
        
                vector<bool> dp(s.size()+1,false);
                dp[0]=true;
        
                vector<int> *vect = new vector<int>[s.size()+1];
                
                for(int i=1;i<=s.size();i++)
                {
                    for(int j=i-1;j>=0;j--)
                    {
                        if(dp[j])
                        {
                            string word = s.substr(j,i-j);
                            if(dict.find(word)!= dict.end())
                            {
                                dp[i]=true;
                                vect[i].push_back(j);
                            }
                        }
                    }
                }
                
    			if(vect[s.size()].size() ==0)
    				return result;
            vector<string> cur;
            dfs(result,vect,s.size(),cur,s);
            
            return result;
}
```