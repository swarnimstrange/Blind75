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

Step 1: Sort the array. Sorting the array makes it possible to use the two-pointer approach.
Step 2: We fix one element nums[i] as the first number of the triplet And make a target sum out of it = 0-nums[i]
Step 3: Place two pointers: left just after i, right at the end of the array
Step 4: We calculate the sum of the two numbers at left and right. Now we compare sum with target (which is -nums[i]).
Step 5: If the sum matches, then (nums[i], nums[left], nums[right]) is a valid triplet. We add it to the set (which ensures uniqueness).
Step 6: If the sum is small, we move left to the right -> this increases the sum (since array is sorted).
Step 7: If the sum is large, we move right to the left -> this decreases the sum.

**Note: Sorting: O(n log n)
Outer loop: O(n)
Inner two-pointer search: O(n)
Total Time Complexity: O(n²) time.
Space Complexity: O(k) for result set (where k is the number of unique triplets).
**

</pre>

<h3> Code in Java </h3>

<pre> 
```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Arrays.sort(nums);
        HashSet<List<Integer>> numSet = new HashSet<>();
        for (int i = 0; i < (nums.length - 2); i++) {
            int target = 0 - nums[i];
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                if (nums[left] + nums[right] == target) {
                    numSet.add(Arrays.asList(nums[i], nums[left], nums[right]));
                    right--;
                    left++;
                } else if (nums[left] + nums[right] > target) {
                    right--;
                } else {
                    left++;
                }
            }
        }
        return new ArrayList<>(numSet);
    }
}
```
</pre>
