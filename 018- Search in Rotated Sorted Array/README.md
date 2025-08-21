<h3> Problem </h3>

There is an integer array nums sorted in ascending order (with distinct values).

Prior to being passed to your function, nums is possibly left rotated at an unknown index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be left rotated by 3 indices and become [4,5,6,7,0,1,2].

Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.

You must write an algorithm with O(log n) runtime complexity.

Example 1:

<pre>

&nbsp;   Input: nums = [4,5,6,7,0,1,2], target = 0

&nbsp;   Output: 4

</pre>


Example 2:

<pre>

&nbsp;   nums = [4,5,6,7,0,1,2], target = 3

&nbsp;   Output: -1

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Divide the array in two parts and keep looping until left <= right.
Step 2: check if left array is sorted. if it is then check if the target falls in that array. if it falls then set right = mid. if it does not falls in that array means it is in right array thus set left = mid+1.
Step 3: if the left array is not sorted it means right array is sorted. thus follow same step as above for right.
Step 4: after every loop keep checking if nums[mid]==target. then return
Step 5: If it comes out of loop then return -1.

**Note: 
Time Complexity = O(logn)
Space Complexity = O(1)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public int search(int[] nums, int target) {
        int left=0;
        int right=nums.length-1;

        while(left<=right){
            int mid = (left+right)/2;
            if(nums[mid]==target){
                return mid;
            }
            if(nums[left]<=nums[mid]){
                if(nums[left] <= target && target <= nums[mid]){
                    right = mid;
                }
                else{
                    left = mid+1;
                }
            }
            else{
                if(nums[mid] < target && target <= nums[right]){
                    left = mid+1;
                }
                else{
                    right = mid;
                }
            }
        }
        return -1;
    }
}
``` </pre>