<h3> Problem </h3>

Given two strings s and t, return true if the two strings are anagrams of each other, otherwise return false.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

Example 1:
<pre>

&nbsp;   Input: s = "racecar", t = "carrace"

&nbsp;   Output: true

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "jar", t = "jam"

&nbsp;   Output: false

</pre>



<h3> Algorithm </h3>

<pre>

Step 1: Initialize two empty HashMaps.

Step 2: Check lengths of both strings, if they're not same return false immedietly

Step 3: If the length is same then store frequencies of both string in HashMap.

Step 4: At last compare both HashMaps if they're equal then return true

**Note: In the loop, it takes O(n) to go through all elements and store their frequencies. runs in O(1) time (amortized) because of the HashMap, Since in this case the HashMap can store up to 26 characters, the space complexity can be considered as O(1).**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public boolean isAnagram(String s, String t) {
        HashMap<Character, Integer> anag1 = new HashMap();
        HashMap<Character, Integer> anag2 = new HashMap();
        int s_length = s.length();
        int t_length = t.length();
        if(s_length!=t_length){
            return false;
        }

        for(int i=0; i<s_length; i++){
            anag1 = getMap(anag1, s, i);
            anag2 = getMap(anag2, t, i);
        }
        if(anag1.equals(anag2)){
            return true;
        }
        return false;
    }

    HashMap<Character, Integer> getMap(HashMap<Character, Integer> anagram, String st, int index){
            if (anagram.containsKey(st.charAt(index))){
                anagram.put(st.charAt(index), anagram.get(st.charAt(index))+1);
            }
            else{
                anagram.put(st.charAt(index), 1);
            }
        return anagram;
    }
} </code> </pre>

