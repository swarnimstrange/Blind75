<h3> Problem </h3>

Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.



Example 1:



<pre>

&nbsp;   Input: nums = [1, 2, 3, 3]

&nbsp;   Output: true

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [1, 2, 3, 4]

&nbsp;   Output: false

</pre>



<h3> Algorithm </h3>

<pre>

Step 1: Initialize an empty HashMap.

Step 2: Loop through each number in the array.

Step 3: If the number already exists in HashMap, return true.

Step 4: Otherwise, add the number to HashMap. After the loop, return false.

**Note: In the loop, it takes O(n) to go through all elements. containsKey runs in O(1) time (amortized) because of the HashMap, so the overall time complexity is O(n). Since the HashMap stores up to n elements, the space complexity is also O(n).**

</pre>



<h3> Code in Java </h3>



<pre><code>  class Solution {
    public boolean containsDuplicate(int[] nums) {
        HashMap<Integer, Integer> checkList = new HashMap<>();
        for (int i : nums){
            if(checkList.containsKey(i)){
                return true;
            }
            checkList.put(i, 1);
        }
        return false;
    }
} </code> </pre>

