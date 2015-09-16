#MaximumProductSubarray
Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.


---




```
方法1
假设数组A中没有0， 最大乘积的值对应subarray在数组中的分布 一定是：
A[0] A[1] .... A[i] 或者 A[j] *A[j+1] A[n - 1]. 

假设有0的话(比如说 A[k] == 0). 那么 A[0],A[1]...A[k - 1 ] 
以及 A[k + 1] A[k + 2]...A[n-1] 可以作为两个新数组来考虑

int maxProduct(int A[], int n)
{
        int frontProduct = 1;
        int backProduct = 1;
        int ans = INT_MIN;
        for (int i = 0; i < n; ++i) {
            frontProduct *= A[i];
            backProduct *= A[n - i - 1];
            ans = max(ans,max(frontProduct,backProduct));
            frontProduct = frontProduct == 0 ? 1 : frontProduct;
            backProduct = backProduct == 0 ? 1 : backProduct;
        }
        return ans;
}
```

```
方法2
int maxProduct(vector<int>& A)
{
         // store the result that is the max we have found so far
        int r = A[0];
    
        // imax/imin stores the max/min product of
        // subarray that ends with the current number A[i]
        for (int i = 1, imax = r, imin = r; i < A.size(); i++) {
            // multiplied by a negative makes big number smaller, small number bigger
            // so we redefine the extremums by swapping them
            if (A[i] < 0)
                swap(imax, imin);
    
            // max/min product for the current number is either the current number itself
            // or the max/min by the previous number times the current one
            imax = max(A[i], imax * A[i]);
            imin = min(A[i], imin * A[i]);
    
            // the newly computed max value is a candidate for our global result
            r = max(r, imax);
         
        }
        return r;
}
```

```

方法2的复杂版本
public int maxProduct(int[] A)
{        
        if(A.length<=0) return 0;  
        if(A.length==1) return A[0];  
        int curMax = A[0];  
        int curMin = A[0];  
        int ans = A[0];  
        for(int i=1;i<A.length;i++){  
            int temp = curMin *A[i];  
            curMin = Math.min(A[i], Math.min(temp, curMax*A[i]));  
            curMax = Math.max(A[i], Math.max(temp, curMax*A[i]));  
            ans = Math.max(ans, curMax);  
        }  
        return ans;
}
```