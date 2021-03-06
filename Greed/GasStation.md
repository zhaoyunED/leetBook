#GasStation
There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next 
station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.


---


```
方法1：
思路：需要从每个点出发来判断是否能围着circle绕一圈,每个点花费时间O(N),总时间复杂度为O(N^2)
这显然不是我们希望的算法时间复杂度
有一个规律我们可以利用： 若是一个station i出发，但是在
x之前停了下来，那么说明了从i+1....x-1之间点 都不能到达x点。
为什么？ 若是 从i可以到达i+1...x-1之间的某一个点k,并且从k能够到达x，那么说明i可以到达x点. 矛盾了

因此只能说明i+1....x-1之间点 都不能到达x点。
那么点i直接跳到了点x而不是i+1,从而整个算法额时间复杂度为O(N)

一下代码摘自leetcode讨论区
int canCompleteCircuit(vector<int>& gas, vector<int>& cost)
{
        int i, j, n = gas.size();

        
        // start from station i
        for (i = 0; i < n; i += j) {
            int gas_left = 0;
            // forward j stations
            for (j = 1; j <= n; j++) {
                int k = (i + j - 1) % n;
                gas_left += gas[k] - cost[k];
                if (gas_left < 0)
                    break;
            }
            if (j > n)
                return i;
        }
        return -1;
}


方法2：

int canCompleteCircuit(vector<int> &gas, vector<int> &cost)
{
        int start = gas.size()-1;
        int end = 0;
       int sum = gas[start] - cost[start];
       while (start > end) {
          if (sum >= 0) {
             sum += gas[end] - cost[end];
             ++end;
          }
          else {
             --start;
             sum += gas[start] - cost[start];
          }
       }
       return sum >= 0 ? start : -1;
}

方法3：
可转换成求循环数组的最大子数组和的问题

```