#MaximumSubarray
Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array [−2,1,−3,4,−1,2,1,−5,4],
the contiguous subarray [4,−1,2,1] has the largest sum = 6.

click to show more practice.

More practice:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach,
which is more subtle.


---
编程之美的上的题目

方法1:
int maxSubArray(int A[], int n) {
        
        if(n<=0)
            return 0;
            
        int maxsum =A[0];
        int sum=0;
        for(int i=0; i<n ; i++)
        {
            sum+=A[i];
            maxsum = sum>maxsum ? sum :maxsum;
            sum = sum>0 ? sum: 0;
        }
        return maxsum;
        
    }
//更容易解释的 DP方法

public int maxSubArray(int[] A) {
        int n = A.length;
        int[] dp = new int[n];//dp[i] means the maximum subarray ending with A[i];
        dp[0] = A[0];
        int max = dp[0];

        for(int i = 1; i < n; i++){
            dp[i] = A[i] + (dp[i - 1] > 0 ? dp[i - 1] : 0);
            max = Math.max(max, dp[i]);
        }

        return max;
} 

//分治方法

int maxSubArray(vector<int>& nums) {
        int result =0;
        result = getMaxSub(nums,0,nums.size()-1);
        return result;
    }
    
int getMaxSub(vector<int>& nums,int left,int right)
{
        if(left >= right ) return nums[left];
        
        int mid = left+(right-left)/2;
        
        int leftans = getMaxSub(nums,left,mid-1);
        int rightans = getMaxSub(nums,mid+1,right);
        
        int leftmax = nums[mid];
        int rightmax =nums[mid];
        
        int temp =0;
        for(int i =mid ;i>=left;i--)
        {
            temp = temp+nums[i];
            leftmax = max(leftmax,temp);
        }
        temp =0;
        for(int i=mid;i<=right;i++)
        {
             temp = temp+nums[i];
            rightmax = max(rightmax,temp);
        }
		int midmax = max(max(leftmax,rightmax),leftmax+rightmax-nums[mid]);
        
        return max(max(leftans,rightans),midmax);
}
