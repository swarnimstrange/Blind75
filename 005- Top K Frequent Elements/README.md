<h3> Problem </h3>

Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:

<pre>

&nbsp;   Input: nums = [1,1,1,2,2,3], k = 2

&nbsp;   Output: [1,2]

</pre>


Example 2:

<pre>

&nbsp;   Input: nums = [1], k = 1

&nbsp;   Output: [1]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Initialize a HashMap<Integer, Integer> to store freq of Elements.
Step 2: Once we have freq we want K most freq elements. for that first loop through K 
Step 3: then initialize largestFreq = 0 because Freq of elements can not be zero so any freq in the Map loop that is stored must be greater that it so it's easy to find out largest Element through looping and largestNum can be find out as largest Element is it's value in hashMap
Step 4: Once we come out of Map loop we have the highest freq number and that element. Store it in return list and then put that element in Map as -1 as it will never come out as Highest freq (because we have already taken it in return loop).
Step 5: After getting all k elements, collect all values in list and return them.

**Note: In the loop, it takes O(n*k) to go through all elements and space comp. is O(n). Since K is the max possible unique numbers present in the list (in worst case scenario it can go to O(n^2) as well) . Therefore it's better as first solution but this can be optimized further to time comp -: O(n) and Space comp. -: O(n)
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> freqMap = new HashMap<> ();
        for(int num: nums){
            if(freqMap.containsKey(num)){
                freqMap.put(num, freqMap.get(num)+1);
            }
            else{
                freqMap.put(num, 1);
            }
        }
        int[] kList = new int[k];
        int largestElement =  0;
        for(int i=0;i<k;i++){
            int largestNum = 0;
            for(Integer num: freqMap.keySet()){
                if(freqMap.get(num)>largestElement){
                    largestElement = freqMap.get(num);
                    largestNum = num;
                }
            }
            freqMap.put(largestNum, -1);
            kList[i] = largestNum;
            largestElement = 0;
        }
        return kList;
    }
} </code> </pre>