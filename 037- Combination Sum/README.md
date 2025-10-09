<h3> Problem </h3>
You are given an array of distinct integers nums and a target integer target. Your task is to return a list of all unique combinations of nums where the chosen numbers sum to target.

The same number may be chosen from nums an unlimited number of times. Two combinations are the same if the frequency of each of the chosen numbers is the same, otherwise they are different.

You may return the combinations in any order and the order of the numbers in each combination can be in any order.

Example 1:

<pre>
    Input: 
    nums = [2,5,6,9] 
    target = 9

    Output: [[2,2,5],[9]]
</pre>

<h3> Algorithm </h3>

<pre>

Step 1: To solve this problem, think of this problem as decision tree approach.
Step 2: Where we have to backtrack for every solution we find, and to eliminate the chance of getting same combination of sequence again.
Step 3: we have to pop out the last element and try to make the solution again with the next element, so that the same kind of seq won't come again. for example -: [[2,2,3],[3,2,2]]
Step 4: so the base condiiton for returning will be that -:
        1 -: when we reach the solution. i.e the sum becomes target, then add the combination of list in listOfList and return
        2 -: when the sum becomes greater than target, then return
        3 -: when index becomes equal to length of nums list, then return.
Step 5: once we return to function, that means either we found the solution, or we have gone out of choice or bound. that menas we will remove the last element and run the same function with next element with same target, so that we can eliminate the risk of getting same combination again.


**Note: 
Time Complexity = O(2^(t/m)) (t is target, m is minimum value in list)
Space Complexity = O(t/m) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    List< List< Integer > > listOfList = new ArrayList<>();
    public List< List< Integer > > combinationSum(int[] nums, int target) {
        List< Integer > list = new ArrayList<>();
        dfs(nums, target, 0, list);
        return listOfList;
    }

    void dfs(int[] nums, int target, int i, List< Integer > list){
        if(target == 0){
            listOfList.add(new ArrayList<>(list));
            return;
        }

        if(i>= nums.length || 0 > target){
            return;
        }

        list.add(nums[i]);
        dfs(nums, target - nums[i], i, list);
        list.remove(list.size() - 1);
        dfs(nums, target, i+1, list);

    }
}
``` </pre>