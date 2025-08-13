<h3> Problem </h3>

Given an array of integers nums, return the length of the longest consecutive sequence of elements that can be formed.

A consecutive sequence is a sequence of elements in which each element is exactly 1 greater than the previous element. The elements do not have to be consecutive in the original array.

You must write an algorithm that runs in O(n) time.

Example 1:

<pre>

&nbsp;   Input: nums = [2,20,4,10,3,4,5]

&nbsp;   Output: 4

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [0,3,2,5,4,6,1,1]

&nbsp;   Output: 7

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: The HashSet version is slightly shorter and avoids storing unnecessary mappings (num -> num+1), so it uses slightly less memory.
Step 3: This is the simpler solution with a HashSet.

**Note: Time Complexity -: O(n+n) = O(n)
Space Complexity -: O(n)
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public int longestConsecutive(int[] nums) {
        HashSet<Integer> numSet = new HashSet<>();
        int maxLength = 0;
        for(int num:nums){
            numSet.add(num);
        }

        for(int num:numSet){

            if(!numSet.contains(num-1)){
                int currentNum = num;
                int length = 0;

                while(numSet.contains(currentNum)){
                    currentNum++;
                    length++;
                }

                if(length>maxLength){
                    maxLength = length;
                }
            }
        }
        return maxLength;
    }
} </code> </pre>