#MergeIntervals
Given a collection of intervals, merge all overlapping intervals.

For example,
Given [1,3],[2,6],[8,10],[15,18],
return [1,6],[8,10],[15,18].


---


```
思路：
先按照起始边从小到大进行排序，之后遍历集合

/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
 
 
static bool compare(const Interval& a, const Interval& b)
        {
            return a.start < b.start;
        }
        
         vector<Interval> merge(vector<Interval>& intervals) 
        {
        
            if(intervals.size()<=0)
                return intervals;
                
            vector<Interval> assist(intervals);
            sort(assist.begin(),assist.end(),compare);
        
            vector<Interval> result;
            result.push_back(assist[0]);
        
            Interval temp =assist[0]; 
            for(int i=1; i< assist.size();i++)
            {
                if(assist[i].start <= temp.end)
                {
                    Interval interval(temp.start,max(temp.end,assist[i].end));
                    result.pop_back();
                    result.push_back(interval);
                    temp = interval;
                }else{
                     result.push_back(assist[i]);
                     temp = assist[i];
                }
            }
        
            return result;
        }
```
