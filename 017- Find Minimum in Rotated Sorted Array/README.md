<h3> Problem </h3>

You are given an array of length n which was originally sorted in ascending order. It has now been rotated between 1 and n times. For example, the array nums = [1,2,3,4,5,6] might become:

[3,4,5,6,1,2] if it was rotated 4 times.
[1,2,3,4,5,6] if it was rotated 6 times.
Notice that rotating the array 4 times moves the last four elements of the array to the beginning. Rotating the array 6 times produces the original array.

Assuming all elements in the rotated sorted array nums are unique, return the minimum element of this array.

A solution that runs in O(n) time is trivial, can you write an algorithm that runs in O(log n) time?

Example 1:

<pre>

&nbsp;   Input: nums = [3,4,5,6,1,2]

&nbsp;   Output: 1

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [4,5,0,1,2,3]

&nbsp;   Output: 0

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Initialize two pointers: left = 0, right = n-1.
Step 2: While left < right:
Step 3: Find middle: mid = (left + right) / 2.
Step 4: Compare nums[mid] with nums[right]: If nums[mid] > nums[right] (It means right array is unsorted and we'll find the smallest element there ) so, set left = mid + 1 Else -> (It means left array is unsorted or fully sorted and we'll find the smallest element there ) so, set right = mid.
Step 5: When loop ends, left == right, pointing to the minimum element.

**Note: 
Time: O(log n) -> binary search.
Space: O(1).
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public int findMin(int[] nums) {
        int left = 0;
        int right = nums.length-1;

        while(left < right){
            int mid = ((right+left)/2);
            if(nums[mid]>nums[right]){
                left = mid + 1;
            }
            else{
                right = mid;
            }
        }
        return nums[left];
    }
}
``` </pre>