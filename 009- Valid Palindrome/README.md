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

Step 1: Initialize two empty StringBuilder objects.
Step 2: Set two pointers: i = 0 and j = s.length() - 1.
Step 3: Loop while i < s.length() and j >= 0:
Step 4: Convert both StringBuilder objects to strings and check if they are equal. If equal then return true, else return false.

**Note: Time Complexity -: Loop: Runs exactly n times (n = s.length()), doing constant-time operations inside O(n) and frontString.toString() and backString.toString() each take O(n) to create new strings so total time Complexity is O(3n) -> O(n).
Space Complexity -: O(n)
**

</pre>

<h3> Code in Java </h3>

<pre><code> class Solution {
    public boolean isPalindrome(String s) {
        StringBuilder frontString = new StringBuilder();
        StringBuilder backString = new StringBuilder();
        int i=0;
        int j=s.length()-1;
        while(i<s.length() && j>=0){
            if(Character.isLetterOrDigit(s.charAt(i))){
                frontString.append(Character.toUpperCase(s.charAt(i)));
            }
            if(Character.isLetterOrDigit(s.charAt(j))){
                backString.append(Character.toUpperCase(s.charAt(j)));
            }
            i++;
            j--;
        }
        if(frontString.toString().equals(backString.toString())){
            return true;
        }
        else{
            return false;
        }
    }
} </code> </pre>