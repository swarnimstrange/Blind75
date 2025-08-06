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

Step 1: Initialize a HashMap<HashMap<Character, Integer>, List<String>> to store anagram groups.
Step 2: For each string, build a frequency map of its characters.
Step 3: If this frequency map already exists in the outer map, add the string to the corresponding group.
Step 4: If not, create a new group with this string and insert it into the map.
Step 5: After processing all strings, collect all values (i.e., groups) from the map and return them.

**Note: In the loop, it takes O(n*m) to go through all elements and store their groups. Since the HashMap<Character, Integer> can store up to 26 characters, the space complexity for this specific map can be considered as O(1). This holds only if you're not storing the full string content in each map value. If each map also stores string references (e.g. in a list), and you're not reusing the same string objects, the total space complexity might become O(n * k) 
where:
n = number of strings
k = average length of a string
**

</pre>

<h3> Code in Java </h3>

<pre><code>  class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<Map<Character, Integer>, List<String>> mapOfM = new HashMap<>();
        for(String str : strs){
            HashMap<Character, Integer> mapOfC = new HashMap<>();
            mapOfC = getFrequencyMap(mapOfC, str);
            if(mapOfM.containsKey(mapOfC)){
                List<String> strList = mapOfM.get(mapOfC);
                strList.add(str);
                mapOfM.put(mapOfC, strList);
            }
            else{
                List<String> stringList = new ArrayList<>();
                stringList.add(str);
                mapOfM.put(mapOfC, stringList);
            }
        }
        List<List<String>> listOfLists = new ArrayList<>(mapOfM.values());
        return listOfLists;
    }

    public HashMap<Character, Integer> getFrequencyMap (HashMap<Character, Integer> mapOfC, String str){
        for(int i=0; i < str.length(); i++){
                Character charStr = str.charAt(i);
                if(mapOfC.containsKey(charStr)){
                    mapOfC.put(charStr, mapOfC.get(charStr)+1);
                }
                else{
                    mapOfC.put(charStr, 1);
                }
            }
        return mapOfC;
    }
} </code> </pre>