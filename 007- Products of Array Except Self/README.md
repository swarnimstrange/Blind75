<h3> Problem </h3>

Given an integer array nums, return an array output where output[i] is the product of all the elements of nums except nums[i].

Each product is guaranteed to fit in a 32-bit integer.

Follow-up: Could you solve it in O(n) time without using the division operation?

Example 1:

<pre>

&nbsp;   Input: nums = [1,2,4,6]

&nbsp;   Output: [48,24,12,8]

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [-1,0,1,2,3]

&nbsp;   Output: [0,-6,0,0,0]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Count zeros and calculate the product of all non-zero elements.
Step 2: If there are more than one zero, result will be all zeros ([0, 0, 0, ...]).
Step 3: If exactly one zero: The position of zero gets the product of all other numbers. All other positions get 0.
Step 4: If no zeros:Use division product / nums[i] to get each output.

**Note: Time Complexity -: O(n+n) = O(n)
Space Complexity -: O(1)
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public int[] productExceptSelf(int[] nums) {
        int zeros = 0;
        int product = 1;
        for(int num:nums){
            if(num != 0){
                product*=num;
            }
            else{
                zeros++;
            }
        }

        if(zeros>1){
            return new int[nums.length];
        }

        for(int i=0; i < nums.length ;i++){
            if(zeros > 0){
                if(nums[i]==0){
                    nums[i] = product;
                }
                else{
                    nums[i] =0;
                }
            }
            else{
                int num = product/nums[i];
                nums[i] = num;
            }
        }
        return nums;
    }
} </code> </pre>