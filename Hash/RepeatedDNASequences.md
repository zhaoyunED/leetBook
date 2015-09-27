#RepeatedDNASequences
All DNA is composed of a series of nucleotides abbreviated as A, C, G, and T, for example: "ACGAATTCCG". 
When studying DNA, it is sometimes useful to identify repeated sequences within the DNA.

Write a function to find all the 10-letter-long sequences (substrings) that occur more than once in a DNA molecule.
```
For example,

Given s = "AAAAACCCCCAAAAACCCCCCAAAAAGGGTTT",

Return:
["AAAAACCCCC", "CCCCCAAAAA"].
```


---


```
思路：要找到所有长度为10的出现两次以上的DNA串
观察ATCG字符的二进制
A:01000001
T:01010100
C:01000011
G:01000111

根据最后三位就可以辨别出来，这样一段段字符串是用最后三位拼接起来

利用 s[i] & 7 得到字符的最后三位,再利用hahsmap来保存已出现过的字符串

vector<string> findRepeatedDnaSequences(string s) {
    unordered_map<int, int> m;
    vector<string> r;
    for (int t = 0, i = 0; i < s.size(); i++)
        if (m[t = t << 3 & 0x3FFFFFFF | s[i] & 7]++ == 1)
            r.push_back(s.substr(i - 9, 10));
    return r;
}
```