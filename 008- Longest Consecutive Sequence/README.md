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

Step 1: You store each number num as a key and map it to num+1.
Step 2: Then, for each number: If it doesn't have a predecessor (num-1 not in map), you start counting forward using the map.
Step 3: This way you only traverse from the start of each consecutive sequence.

**Note: Time Complexity -: O(n+n) = O(n)
Space Complexity -: O(n)
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public int longestConsecutive(int[] nums) {
        HashMap<Integer, Integer> numMap = new HashMap<>();
        for(int num: nums){
            numMap.put(num, num+1);
        }
        
        int maxCount = 0;
        for(int num:numMap.keySet()){
            int count = 0;
            if(!numMap.containsKey(num-1)){
                int currentNum = num;
                int length = 0;

                while(numMap.containsKey(currentNum)){
                    currentNum = numMap.get(currentNum);
                    count++;
                }
                if(count>maxCount){
                    maxCount=count;
                }
            }
        }
        return maxCount;
    }
} </code> </pre>