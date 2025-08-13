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

Step 1: Initialize an output array with size n.
Step 2: Prefix pass: Set output[0] = 1. For each i from 1 to n-1, set output[i] = output[i-1] * nums[i-1] (stores the product of all elements before i)
Step 3: Suffix pass: Keep a suffix = 1. Iterate i from n-1 down to 0: Multiply output[i] by suffixProduct. Update suffixProduct *= nums[i](This adds the product of all elements after i).
Step 4: Return the output array — now each output[i] is the product of all elements except nums[i].

**Note: Time Complexity -: O(n+n) = O(n)
Space Complexity -: O(1) (if we exclude output return array).
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] output = new int[nums.length];
        output[0] = 1;
        for(int i =1; i< nums.length ; i++){
            output[i] = output[i-1] * nums[i-1];
        }
        
        int suffix=1;
        for(int i=nums.length-1 ; i>=0 ; i--){
            output[i] *= suffix;
            suffix *= nums[i]; 
        }
        return output;
    }
} </code> </pre>