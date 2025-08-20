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

Step 1: Start by buying at day 0. buyingIndex = 0 (first day). sellingIndex = 1 (next day).
Step 2: Move forward the selling day (as long as price keeps going up).
Step 3: Whenever price drops, reset your buying day to that point. Reset buyingIndex to the current sellingIndex and Move sellingIndex to the next day after that.
Step 4: Keep track of the maximum profit seen along the way, return maximum profit once it comes out of loop.

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
        int maxProfit = 0;
        int buyingIndex = 0;
        int sellingIndex = 1;
        while(sellingIndex<prices.length){
            while(prices[sellingIndex]>=prices[buyingIndex]){
                int profit = prices[sellingIndex]-prices[buyingIndex];
                if(profit>maxProfit){
                    maxProfit = profit;
                }
                if(sellingIndex==prices.length-1){
                    break;
                }
                sellingIndex++;
            }
            buyingIndex = sellingIndex;
            sellingIndex = sellingIndex+1;
        }
        return maxProfit;
    }
}
``` </pre>