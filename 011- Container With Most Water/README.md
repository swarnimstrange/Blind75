<h3> Problem </h3>

Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] where nums[i] + nums[j] + nums[k] == 0, and the indices i, j and k are all distinct.

The output should not contain any duplicate triplets. You may return the output and the triplets in any order.

Example 1:

<pre>

&nbsp;   Input: nums = [-1,0,1,2,-1,-4]

&nbsp;   Output: [[-1,-1,2],[-1,0,1]]

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [0,1,1]

&nbsp;   Output: []

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Initialize left starts at the beginning of the array, right at the end of the array. we'll shrink the window step by step to find the maximum area.
Step 2: loop unitl left is lesser than right.
Step 3: Compare the heights. 
Step 4: If height[left] > height[right], then smaller line determines water level. So, compute area with height[right]. Then move right-- inward, hoping to find a taller line.
Step 4: Else if height[left] <= height[right], compute area with height[left]. Then move left++ inward, hoping to find a taller line.
Step 5: Return the max found area.

**Note: 
Time Complexity = O(n) (we scan the array once).
Space Complexity = O(1).
**

</pre>

<h3> Code in Java </h3>

<pre><code> class Solution {
    public int maxArea(int[] height) {
        int left = 0;
        int right = height.length-1;
        int maxArea = 0;
        while(left<right){
            if(height[left]>height[right]){
                int area = height[right] * (right-left);
                if(area > maxArea){
                    maxArea = area;
                }
                right--;
            }
            else{
                int area = height[left] * (right-left);
                if(area > maxArea){
                    maxArea = area;
                }
                left++;
            }
        }
        return maxArea;
    }
}</code> </pre>