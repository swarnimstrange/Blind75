<h3> Problem </h3>

Given a string s, return true if it is a palindrome, otherwise return false.

A palindrome is a string that reads the same forward and backward. It is also case-insensitive and ignores all non-alphanumeric characters.

Note: Alphanumeric characters consist of letters (A-Z, a-z) and numbers (0-9).

Example 1:

<pre>

&nbsp;   Input: s = "Was it a car or a cat I saw?"

&nbsp;   Output: true

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "tab a cat"

&nbsp;   Output: false

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Set two pointers: left at start, right at end.
Step 2: Skip all non-alphanumeric characters from the left side until you find a valid one.
Step 3: Skip all non-alphanumeric characters from the right side until you find a valid one.
Step 4: Convert both characters to uppercase and compare them. If they don't match then return false.
Step 5: Move left forward and right backward, and repeat steps 2-4 until left >= right.
Step 6: If the loop finishes without mismatches then return true (it's a palindrome).

**Note: This one is O(n) time and O(1) space, since it compares in-place without building new strings.
**

</pre>

<h3> Code in Java </h3>

<pre><code> class Solution {
    public boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length()-1;

        while(left<right){
            while(left<right && !Character.isLetterOrDigit(s.charAt(left))){
                left++;
            }

            while(left<right && !Character.isLetterOrDigit(s.charAt(right))){
                right--;
            }

            Character leftChar = Character.toUpperCase(s.charAt(left));
            Character rightChar = Character.toUpperCase(s.charAt(right));
            if(leftChar!=rightChar){
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
} </code> </pre>