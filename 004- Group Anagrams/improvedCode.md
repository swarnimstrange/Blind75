<h3> Problem </h3>

Given an array of strings strs, group all anagrams together into sublists. You may return the output in any order.

An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

Example 1:

<pre>

&nbsp;   Input: strs = ["act","pots","tops","cat","stop","hat"]

&nbsp;   Output: [["hat"],["act", "cat"],["stop", "pots", "tops"]]

</pre>


Example 2:

<pre>

&nbsp;   Input: strs = ["x"]

&nbsp;   Output: [["x"]]

</pre>

<h3> Algorithm </h3>

<pre>

int[] count = new int[26];
This line creates a new integer array of size 26 (for 26 letters: 'a' to 'z'), and in Java, arrays of primitives are automatically initialized to 0.
Is equivalent to -: int[] count = {0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0};

Then this line:
<b> count[c - 'a']++; </b>
Starts modifying the appropriate index

For string "eat": [1,0,0,0,1,...,1,...]

Then this line:
<b> sb.append((char) ('a' + i)).append(count[i]); </b>
Converts index back to a character and append the cound of frequency

So we get a string like this, which can be compared -: "a1e1t1"

Time & Space Complexity -: 
this code is a little better than before even thought the time and space complexity of both codes are same. i.e  O(n*m) 
For previous code -:The JVM has to call .hashCode() and .equals() on the entire Map<Character, Integer> object, These are relatively heavy operations. Map objects are heap-allocated, and comparison between maps involves comparing both keys and values

**Note: This solution generates a simple, immutable String as key. Strings in Java have fast and optimized hashCode() and equals(). Much less overhead than comparing entire Map structures. Therefore it is faster.
**

</pre>

<h3> Code in Java </h3>

<pre><code> class Solution {
    public String getSignature(String s) {
        int[] count = new int[26];
        for (char c : s.toCharArray()) {
            count[c - 'a']++;
        }

        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < 26; i++) {
            if (count[i] != 0) {
                sb.append((char) ('a' + i)).append(count[i]);
            }
        }
        return sb.toString();
    }

    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new ArrayList<>();
        Map<String, List<String>> groups = new HashMap<>();

        for (String s : strs) {
            groups.computeIfAbsent(getSignature(s), k -> new ArrayList<>()).add(s);
        }

        result.addAll(groups.values());

        return result;
    }
} </code> </pre>
