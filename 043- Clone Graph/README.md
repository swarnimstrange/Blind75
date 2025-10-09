<h3> Problem </h3>
Given a node in a connected undirected graph, return a deep copy of the graph.

Each node in the graph contains an integer value and a list of its neighbors.

<pre>
class Node {
    public int val;
    public List< Node > neighbors;
}
</pre>

The graph is shown in the test cases as an adjacency list. An adjacency list is a mapping of nodes to lists, used to represent a finite graph. Each list describes the set of neighbors of a node in the graph.

For simplicity, nodes values are numbered from 1 to n, where n is the total number of nodes in the graph. The index of each node within the adjacency list is the same as the node's value (1-indexed).

The input node will always be the first node in the graph and have 1 as the value.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/ca68c09d-4d0e-4d80-9c20-078c666cf900/public">
    Input: adjList = [[2],[1,3],[2]]

    Output: [[2],[1,3],[2]]

</pre>

Example 2:

<pre>
    Input: adjList = [[]]

    Output: [[]]

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: To make a clone of a graph, make a map such that realMap elements are connected to new clone elements. It is neccesary because one of the base condition will be that if the clone of that neighbour is already available then we can directly return the node and not create it again multiple times.
Step 2: once we have the clone Map, we can do the usual graph dfs traversal and keep creating the node as we traverse and if already available then return that node and once cover all the node we we have our clone graph created


**Note: 
Time Complexity = O(V+E)
Space Complexity = O(V+E)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashMap< Node, Node > copyMap = new HashMap<>();
    public Node cloneGraph(Node node) {
        if(node == null){
            return null;
        }
        if(copyMap.containsKey(node)){
            return copyMap.get(node);
        }
        Node cur = new Node(node.val);
        copyMap.put(node, cur);
        for(Node nei: node.neighbors){
            cur.neighbors.add(cloneGraph(nei));
        }
        return cur;
    }
}
``` </pre>