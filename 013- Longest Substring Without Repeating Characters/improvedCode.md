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

Step 1: Use map to store each character's last seen index.
Step 2: If a duplicate c is found at index i, Move left pointer just past the last occurrence of c. left = Math.max(left, map.get(c) + 1) ensures left only moves forward.
Step 3: Update map.put(c, i) with the current index of c.
Step 4: Calculate window length as i - left + 1.

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
        HashMap<Character, Integer> map = new HashMap<>();
        int left = 0;

        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);

            // If we saw this character before, jump left pointer
            if (map.containsKey(c)) {
                left = Math.max(left, map.get(c) + 1);
            }

            // Update character's latest index
            map.put(c, i);

            // Update max length
            maxLength = Math.max(maxLength, i - left + 1);
        }

        return maxLength;
    }
}
``` </pre>