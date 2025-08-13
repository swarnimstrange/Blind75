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

Step 1 - iterate through the array nums once. and put their freq in the map
Step 2 - Create Bucket and loop freqMap length and using freq as index put numbers in buckets.
Step 3 - Collect top K frequent elements by looping from backward direction and putting the numbers in new Array and once we reach K return the array


Time & Space Complexity -: 
this code is better than before because now it's taking liner time O(n) to complete the program. Also the space complexity is O(n)


**Note: In between the code we can see a bit of nested loop. But even in the worst case it can be max O(n). Even if the bucket array of size n+1 and worst case in this is that there's no repetition of element then K can be maximum 1. vice-versa can also be same so worst case is O(n).
**

</pre>

<h3> Code in Java </h3>

<pre><code> class Solution {
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
        List<Integer>[] result = new List[nums.length + 1];
        for(int num: freqMap.keySet()){
            if(result[freqMap.get(num)] == null){
                result[freqMap.get(num)] = new ArrayList<>();
            }
            result[freqMap.get(num)].add(num);
        }

        int[] kList = new int[k];
        int index = 0;
        for(int i = result.length-1; i >0 && index<k; i--){
            if (result[i] != null) {
                for(int item : result[i]){
                    kList[index] = item;
                    index++;
                } 
            }
        }
        return kList;
    }
}
</code> </pre>