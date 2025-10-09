<h3> Problem </h3>
There is an undirected graph with n nodes. There is also an edges array, where edges[i] = [a, b] means that there is an edge between node a and node b in the graph.

The nodes are numbered from 0 to n - 1.

Return the total number of connected components in that graph.

Example 1:

<pre>
    Input:  n=3
    edges=[[0,1], [0,2]]

    Output: 1
</pre>

Example 2:

<pre>
    Input:  n=6
    edges=[[0,1], [1,2], [2,3], [4,5]]

    Output: 2
</pre>

<h3> Algorithm </h3>

<pre>

Step 1: this is kinda same compared to the logic of valid graph tree. In that code we were checking that if any independent nodes are present or not.
Step 2: we have to do the same here. instead of returning false like valid graph tree, we have to increment everytime we counter an independent node.
Step 3: this will give us total number of connected components in undirected graph.


**Note: 
Time Complexity = O(V+E)
Space Complexity = O(V+E)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashMap< Integer, List< Integer>> graphMap = new HashMap<>();
    HashSet< Integer> visited = new HashSet<>();
    public int countComponents(int n, int[][] edges) {
        int count=0;
        if(n==0){
            return 0;
        }
        for(int i=0; i< n; i++){
            graphMap.put(i, new ArrayList<>());
        }

        for(int[] edge: edges){
            graphMap.get(edge[0]).add(edge[1]);
            graphMap.get(edge[1]).add(edge[0]);
        }

        for(int i=0; i< n; i++){
            if(!visited.contains(i)){
                count++;
                dfs(i, -1);
            }
        }
        return count;
    }

    public void dfs(int node, int parentNode){
        if(visited.contains(node)){
            return;
        }

        visited.add(node);
        for(int curNode: graphMap.get(node)){
            if(curNode == parentNode){
                continue;
            }
            else{
                dfs(curNode, node);
            }
        }
    }
}
``` </pre>