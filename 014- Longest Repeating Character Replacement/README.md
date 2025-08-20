<h3> Problem </h3>

You are given a string s consisting of only uppercase english characters and an integer k. You can choose up to k characters of the string and replace them with any other uppercase English character.

After performing at most k replacements, return the length of the longest substring which contains only one distinct character.

Example 1:

<pre>

&nbsp;   Input: s = "XYYX", k = 2

&nbsp;   Output: 4

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "AAABABB", k = 1

&nbsp;   Output: 5

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: We need to track few things for this solution -:
    left -> right => current window size.
    count[26]: frequency of A -> Z inside the window.
    maxFreq: the highest frequency of any letter in the window.
    maxLenght: best window length seen so far.
Step 2: Start with left = 0, result = 0, maxFreq = 0, all counts = 0.
Step 3: For each right from 0 to n-1: Add s[right] to the count array and Update maxFreq = max(maxFreq, intArray[index]).
Step 4: While (right - left + 1) - maxFreq > k, shrink from the left: Decrease count[s[left]], and move left++. (so that we find a better window size where we can fit k element).
Step 5: Update maxLength = max(maxLength, right - left + 1).

**Note: 
Time Complexity = O(n)
Space Complexity = O(1) (We use int[] count = new int[26] -> constant size, O(1).)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public int characterReplacement(String s, int k) {
        int maxFreq= 0;
        int maxLength = 0;
        int left = 0;
        int[] intArray = new int[26];
        for(int right=0;right<s.length();right++){
            int index = s.charAt(right) - 'A';
            intArray[index]++;
            maxFreq = Math.max(maxFreq, intArray[index]);

            while((right-left+1)-maxFreq >k){
                int indx = s.charAt(left) - 'A';
                intArray[indx]--;
                left++;
            }
            maxLength = Math.max(maxLength, right-left+1);
        }
        return maxLength;
    }
}
``` </pre>