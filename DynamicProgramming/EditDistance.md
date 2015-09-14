#EditDistance
Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character

b) Delete a character

c) Replace a character


---
思路：老题目了

方法1 O(mn)的空间

distance[i][j]表示word1[0..i]与word2[0..j]大的最小距离

我们可以得到动规方程：

当word1[i-1] == word2[j-1] distance[i][j] = distance[i-1][j-1];

当word1[i-1] ！= word2[j-1]
distance[i][j] = 1+ min(distance[i-1][j-1], distance[i-1][j], distance[i][j-1])

```
int minDistance(string word1, string word2)
{
       vector<vector<int>> distance(word1.length()+1, vector<int>(word2.length()+1, 0));
       
       for(int i=0;i<=word1.length();i++)
            distance[i][0]=i;
       for(int i=0;i<=word2.length();i++)
            distance[0][i]=i;
     
     // when insert a char to word1 it means we are trying to match word1 at i-1 to word2 at j
     // when delete a char from word1 it equals to insert a char to word2, which
     // means we are trying to match word1 at i to word2 at j-1
     // when replace a char to word1, then we add one step to previous i and j
       for(int i=1; i< distance.size(); i++)
       for(int j=1; j<distance[0].size(); j++){
            if(word1[i-1] == word2[j-1])
                distance[i][j] = distance[i-1][j-1];
            else
                distance[i][j] = 1+ min(distance[i-1][j-1], min(distance[i-1][j], distance[i][j-1]));//important to understand
        }
        
        return distance[word1.length()][word2.length()];
}
```

方法2：
O(n)的空间复杂度

f[i][j] 只依赖 f[i-1][j-1], f[i-1][j] 和 f[i][j-1] ，我们可以把算法的空间复杂度降到O(n)



```
int minDistance(string word1, string word2)
{
        int l1 = word1.size();
        int l2 = word2.size();

        vector<int> f(l2+1, 0);
        for (int j = 1; j <= l2; ++j)
            f[j] = j;

        for (int i = 1; i <= l1; ++i)
        {
            int prev = i;
            for (int j = 1; j <= l2; ++j)
            {
                int cur;
                if (word1[i-1] == word2[j-1]) {
                    cur = f[j-1];
                } else {
                    cur = min(min(f[j-1], prev), f[j]) + 1;
                }

                f[j-1] = prev;
                prev = cur;
            }
            f[l2] = prev;
        }
        return f[l2];
}
```