<h3> Problem </h3>
There is a foreign language which uses the latin alphabet, but the order among letters is not "a", "b", "c" ... "z" as in English.

You receive a list of non-empty strings words from the dictionary, where the words are sorted lexicographically based on the rules of this new language.

Derive the order of letters in this language. If the order is invalid, return an empty string. If there are multiple valid order of letters, return any of them.

A string a is lexicographically smaller than a string b if either of the following is true:

The first letter where they differ is smaller in a than in b.
a is a prefix of b and a.length < b.length.

Example 1:

<pre>
    Input: ["z","o"]

    Output: "zo"

</pre>

Example 2:

<pre>
    Input: ["hrn","hrf","er","enn","rfnn"]

    Output: "hernf"

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: Loop through all words and all letters. Add every letter as a node in: adjMap and indegree Map. (Ensures every character appears in the graph, even if it has no edges.)
Step 2: Compare each pair of adjacent words. Find the first position j where they differ: Then add edge c1 → c2 (meaning c1 comes before c2). Increase indegree of c2 by 1
Step 3: If one word is a prefix of another (e.g. "abc", "ab"), invalid order → return ""
Step 4: Initialize topological sort. Add all nodes with indegree == 0 to a queue.
Step 5: Perform Kahn’s Algorithm: While queue not empty: Pop one node. Append it to the result string. For each neighbor: Decrease its indegree by 1. If indegree becomes 0 → push to queue.
Step 6: Validate & return: If result length < total unique letters → there’s a cycle → return "". Otherwise, return the built string.

**Note: 
Time Complexity = O(V+E)
Space Complexity = O(V+E)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashMap< Character, List< Character>> adjMap = new HashMap<>();
    HashMap< Character, Integer> incmEdgesMap = new HashMap<>();
    public String foreignDictionary(String[] words) {
        int n = words.length;
        for(String word: words){
            for(char c: word.toCharArray()){
                adjMap.putIfAbsent(c, new ArrayList<>());
                incmEdgesMap.putIfAbsent(c, 0);
            }
        }

        for(int i=0; i< n-1; i++){
            String word1 = words[i];
            String word2 = words[i+1];
            int lowestLength = Math.min(word1.length(), word2.length());
            int index=0;
            while(index < lowestLength){
                if(word1.charAt(index) != word2.charAt(index)){
                    char c1 = word1.charAt(index);
                    char c2 = word2.charAt(index);
                    adjMap.get(c1).add(c2);
                    incmEdgesMap.put(c2, incmEdgesMap.get(c2)+1);
                    break;
                }
                index++;
            }
            if(index == lowestLength && word1.length() > word2.length()){
                return "";
            }
        }
        String topoString = topologicalSort();
        return topoString.length() < incmEdgesMap.size() ? "" : topoString;
    }

    public String topologicalSort(){
        StringBuilder topoStr = new StringBuilder();
        Queue< Character> queue = new LinkedList<>();
        for(Character node: incmEdgesMap.keySet()){
            if(incmEdgesMap.get(node) == 0){
                queue.add(node);
            }
        }
        while(!queue.isEmpty()){
            char node = queue.peek();
            for(char adjNode: adjMap.get(node)){
                incmEdgesMap.put(adjNode, incmEdgesMap.get(adjNode)-1);
                if(incmEdgesMap.get(adjNode) == 0){
                    queue.add(adjNode);
                }
            }
            topoStr.append(node);
            queue.remove();
        }
        return topoStr.toString();
    }
}
``` </pre>