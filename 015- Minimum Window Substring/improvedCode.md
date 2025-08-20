<h3> Problem </h3>

Given two strings s and t, return the shortest substring of s such that every character in t, including duplicates, is present in the substring. If such a substring does not exist, return an empty string "".

You may assume that the correct output is always unique.

Example 1:

<pre>

&nbsp;   Input: s = "OUZODYXAZV", t = "XYZ"

&nbsp;   Output: "YXAZ"

</pre>


Example 2:

<pre>

&nbsp;   Input: s = "xyz", t = "xyz"

&nbsp;   Output: "xyz"

</pre>


<h3> Algorithm </h3>

<pre>

Logic is same as readme, only change is in Space complexity which is better.

**Note: 
Time Complexity = O(n)
Space Complexity = O(1) (new int[128] -> constant size, O(1) better for larger inputs)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public String minWindow(String s, String t) {
        int[] need = new int[128]; // or 256 if Unicode
        int[] window = new int[128];
        
        int needCount = 0; // number of unique chars in t
        for (char c : t.toCharArray()) {
            if (need[c] == 0) needCount++;
            need[c]++;
        }

        int have = 0;
        int left = 0, start = 0, minLen = Integer.MAX_VALUE;

        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            window[c]++;

            if (need[c] > 0 && window[c] == need[c]) {
                have++;
            }

            while (have == needCount) {
                if (right - left + 1 < minLen) {
                    minLen = right - left + 1;
                    start = left;
                }
                char leftChar = s.charAt(left);
                window[leftChar]--;
                if (need[leftChar] > 0 && window[leftChar] < need[leftChar]) {
                    have--;
                }
                left++;
            }
        }
        return minLen == Integer.MAX_VALUE ? "" : s.substring(start, start + minLen);
    }
}
``` </pre>