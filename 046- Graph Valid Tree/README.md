<h3> Problem </h3>
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to check whether these edges make up a valid tree.

Example 1:

<pre>
    Input:  n = 5
    edges = [[0, 1], [0, 2], [0, 3], [1, 4]]

    Output: true
</pre>

Example 2:

<pre>
    Input:  n = 5
    edges = [[0, 1], [1, 2], [2, 3], [1, 3], [1, 4]]

    Output: false
</pre>

<h3> Algorithm </h3>

<pre>

Step 1: One thing to keep in mind before solving this problem is that, basically it's a combination of nodes where whenever we encounter a cycle between nodes, then that means, it not tree.
Step 2: And if we encounter independent nodes that are disconnected from each other, in that case also we can say that it's not a valid tree.
Step 3: to detect cycle, visit every node one by one, and visited add it to visited set.
Step 4: If we counter anything that is present in the visited node that basically means we have found the a cycle hence return false
Step 5: After we finish exploring and compare visited and number of nodes if there are some differences, then that means some nodes are not traversed due to being independent. hence return false in that case else return true.


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
    Set< Integer> visited = new HashSet<>();
    public boolean validTree(int n, int[][] edges) {
        for(int i=0; i < n; i++){
            graphMap.put(i, new ArrayList<>());
        }

        for(int[] edge: edges){
            graphMap.get(edge[0]).add(edge[1]);
            graphMap.get(edge[1]).add(edge[0]);
        }
        
        System.out.println(graphMap);
        if(!dfs(0, -1)){
            return false;
        }

        return visited.size() != n ? false : true;
    }

    public boolean dfs(int node, int prevNode){
        if(visited.contains(node)){
            return false;
        }
        visited.add(node);
        for(int neighbour: graphMap.get(node)){
            if(prevNode == neighbour){
                continue;
            }
            else{
                if(!dfs(neighbour, node)){
                    return false;
                }
            }
        }
        return true;
    }
}

``` </pre>