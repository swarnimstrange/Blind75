<h3> Problem </h3>

Given a string s, find the length of the longest substring without duplicate characters.

A substring is a contiguous sequence of characters within a string.

Example 1:

<pre>

&nbsp;   Input: s = "zxyzxyz"

&nbsp;   Output: 3

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "xxxx"

&nbsp;   Output: 1

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Loop through each character using i as the right pointer. Current character is c = s[i].
Step 2: If c is already in the set (meaning we found a duplicate), Shrink the window from the left until the duplicate is removed. Each time we remove a character, we decrement count and move left forward.
Step 3: Whenever price drops, reset your buying day to that point. Reset buyingIndex to the current sellingIndex and Move sellingIndex to the next day after that. This ensures the substring [left ... i] always contains unique characters.
Step 4: Add the current character c to the set. Increase the count (unique characters in window). Update maxLength if the current window length (count) is bigger.
Step 5: Move right pointer (i) forward and repeat until end of string. Return the maximum length once code is out of loop.

**Note: 
Time: O(n) -> each character is added and removed from the set at most once.
Space: O(m) ->  where m is the number of unique characters in the string.
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int maxLength = 0;
        HashSet<Character> letterSet = new HashSet<>();
        int count=0;
        int left=0;
        int i = 0;
        while(i<s.length()){
            char c= s.charAt(i);
            while(letterSet.contains(c)){
                letterSet.remove(s.charAt(left));
                left++;
                count -= 1;
            }
            letterSet.add(c);
            count++;
            if(count>maxLength){
                maxLength = count;
            }
            i++;
        }
        return maxLength;
    }
}
``` </pre>