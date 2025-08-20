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

Step 1: We need to track few things for this solution -:
    HashMap<Character, Integer> needMap = new HashMap<>();
    HashMap<Character, Integer> windowMap = new HashMap<>();
    int currHave = 0;
    int needHave = 0;
    int minValue = 9999;
    int left = 0;
    int start = 0;
Step 2: Count the frequency of each character in t (because duplicates matter). Example: t = "AABC" -> {A=2, B=1, C=1}
Step 2: Use two pointers (left, right) to represent a window in s.
Step 3: Expand right step by step: Keep adding characters into the current window's frequency count
Step 4: When the window satisfies all required characters, try to shrink it from the left side to make it as small as possible.
Step 5: Track the minimum window size + substring along the way.

**Note: 
Time Complexity = O(n)
Space Complexity = O(m) (where m is the maximum unique number in String) or O(1) (if we use new int[128] -> constant size, O(1) better for larger inputs)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> needMap = new HashMap<>();
        HashMap<Character, Integer> windowMap = new HashMap<>();
        int currHave = 0;
        int needHave = 0;
        int minValue = 9999;
        int left = 0;
        int start = 0;

        for(int i=0;i<t.length();i++){
            char c = t.charAt(i);
            needMap.put(c, needMap.getOrDefault(c, 0) + 1);
        }
        needHave = needMap.size();

        for(int i=0;i<s.length();i++){
            char currChar = s.charAt(i);
            windowMap.put(currChar, windowMap.getOrDefault(currChar, 0) + 1);

            if(needMap.containsKey(currChar) && needMap.get(currChar)==windowMap.get(currChar)){
                currHave++;
            }

            while(currHave == needHave){
                if((i-left+1)<minValue){
                    minValue = i-left+1;
                    start = left;
                }

                char leftChar = s.charAt(left);
                windowMap.put(leftChar, windowMap.get(leftChar)-1);
                if(needMap.containsKey(leftChar) && windowMap.get(leftChar)<needMap.get(leftChar)){
                    currHave--;
                }
                left++;
            }
        }
        if(minValue==9999){
            return "";
        }
        else{
            return s.substring(start, start+minValue);
        }
    }
}
``` </pre>