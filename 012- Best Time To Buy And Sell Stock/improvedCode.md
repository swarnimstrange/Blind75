<h3> Problem </h3>

You are given an integer array prices where prices[i] is the price of NeetCoin on the ith day.

You may choose a single day to buy one NeetCoin and choose a different day in the future to sell it.

Return the maximum profit you can achieve. You may choose to not make any transactions, in which case the profit would be 0.

Example 1:

<pre>

&nbsp;   Input: prices = [10,1,5,6,7,1]

&nbsp;   Output: 6

</pre>


Example 2:

<pre>

&nbsp;   Input: prices = [10,8,7,5,2]

&nbsp;   Output: 0

</pre>


<h3> Algorithm </h3>

<pre>
Previous version uses nested while, which is a bit more complex than necessary.
The standard cleaner approach is throught Dynamic Programming.

Step 1: Initialize values : minPrice keeps track of the lowest price so far (best day to buy). maxProfit stores the best profit found so far.
Step 2: Iterate over prices starting from day 1
Step 4: Check possible profit by prices[i] - minPrice. Compare it with the current maxProfit, update if it's better.
Step 3: Find the lowest minimum value in every iteration and compare it with the current minimum value, update if it's lower.
Step 5: After scanning all days, return the best profit found.

**Note: 
Time: O(n) (each index is visited at most twice).
Space: O(1).
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = prices[0];
        int maxProfit = 0;
        for (int i = 1; i < prices.length; i++) {
            maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }
        return maxProfit;
    }
}
``` </pre>