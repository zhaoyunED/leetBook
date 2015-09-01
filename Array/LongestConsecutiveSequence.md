
# longestConsecutiveSequence

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.

Your algorithm should run in O(n) complexity.


---
思路：

用一个map来存每个元素所在的最长连续序列的长度。
对于数组中的每个数s,找 s-1 与 s+1 的序列长度,分别为left，right，最终s所在最长连续序列的长度即为left+right+1


 ```
 int longestConsecutive(vector<int>& nums) {
        unordered_map<int, int> m;
        int r = 0;
        
        for(int s:nums)
        {
            if(m[s]) continue;
            
            int left = (m.find(s-1) == m.end()) ? 0: m[s-1];
            int right = (m.find(s+1) == m.end()) ? 0: m[s+1];
            
            int leng = right +left +1;
            m[s] =leng;
            
            r = max(leng,r);
            
            m[s-left] = leng;
            m[s+right] = leng;
        }
        return r;
}
```

精简版代码

```
int longestConsecutive(vector<int> &num)
{
    unordered_map<int, int> m;
    int r = 0;
    for (int i : num) {
        if (m[i]) continue;
        r = max(r, m[i] = m[i + m[i + 1]] = m[i - m[i - 1]] = m[i + 1] + m[i - 1] + 1);
    }
    return r;
}
```