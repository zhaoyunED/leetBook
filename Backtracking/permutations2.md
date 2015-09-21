#Permutation2
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

For example,
[1,1,2] have the following unique permutations:
[1,1,2], [1,2,1], and [2,1,1].



```

思路：
若是用num的引用 并且 递归完仍然swap(num[i], num[k]) 是会出现重复的结果
这是和题目Permutation不同的地方

void recursion(vector<int> num, int i, int j, vector<vector<int> > &res) 
{
        if (i == j-1) {
            res.push_back(num);
            return;
        }
        for (int k = i; k < j; k++) {
            if (i != k && num[i] == num[k]) continue;
            swap(num[i], num[k]);
            recursion(num, i+1, j, res);
        }
}

vector<vector<int> > permuteUnique(vector<int> &num) 
{
        sort(num.begin(), num.end());
        vector<vector<int> >res;
        recursion(num, 0, num.size(), res);
        return res;
}
```