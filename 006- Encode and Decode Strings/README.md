<h3> Problem </h3>

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

Please implement encode and decode

Example 1:

<pre>

&nbsp;   Input: ["neet","code","love","you"]

&nbsp;   Output:["neet","code","love","you"]

</pre>


Example 2:

<pre>

&nbsp;   Input: ["we","say",":","yes"]

&nbsp;   Output: ["we","say",":","yes"]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1: Initialize an empty string finalString which will store the encoded version of the array of strings.
Step 2: Loop through each string in the input array.
Step 3: For each string, append its length to finalString, followed by a delimiter "-", then append the string itself. 
for example -: ["cat", "hello"] -> "3-cat5-hello"

For Decode -:
Step 1: Initialize an empty List<String> to store decoded strings.
Step 2: Start a pointer i at index 0 of the encoded string. Loop until i reaches the end of the encoded string.
Step 3: Initialize another pointer j at i and move it forward until you find the "-" delimiter.
Step 4: Convert the substring from i to j to an integer lengthOfS (length of the next word).
Step 5: Move j forward by 1 (to skip the delimiter).
Step 6: Extract the substring from j to j + lengthOfS and add it to stringList.
Step 7: Update i to point right after the extracted word (i = j + lengthOfS).
Step 8: Once all strings are decoded, convert stringList to a String[] and return it.

**Note: For Encoding Time complexity is -: O(n) and Space complexity is -:O(1)
For Decoding Time complexity is -: O(n) and Space complexity is -:O(m)
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {

    public String encode(String s[]) {
        String finalString = "";
        for(String str: s){
            finalString += String.valueOf(str.length());
            finalString += "-";
            finalString += str;
        }
        return finalString;
    }

    public String[] decode(String s) {
        List<String> stringList = new ArrayList<>();
        int i = 0;
        while(i < s.length()){
            int j = i;
            while(s.charAt(j)!='-'){
                j++;
            }
            int lengthOfS = Integer.parseInt(s.substring(i,j));
            j++;
            String getString = s.substring(j, j+lengthOfS);
            stringList.add(getString);
            i = j+lengthOfS;
        }
        return stringList.toArray(new String[0]);
    }
} </code> </pre>