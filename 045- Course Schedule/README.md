<h3> Problem </h3>
You are given an array prerequisites where prerequisites[i] = [a, b] indicates that you must take course b first if you want to take course a.

The pair [0, 1], indicates that must take course 1 before taking course 0.

There are a total of numCourses courses you are required to take, labeled from 0 to numCourses - 1.

Return true if it is possible to finish all courses, otherwise return false.

Example 1:

<pre>
    Input: numCourses = 2, prerequisites = [[0,1]]

    Output: true

</pre>

Example 2:

<pre>
    Input: numCourses = 2, prerequisites = [[0,1],[1,0]]

    Output: false

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: One thing to keep in mind before solving this problem is that, basically it's a combination of nodes where whenever we encounter a cycle between nodes, then that means, the prerequisited cannot be completed because od cyclic dependency.
Step 2: So, detecting a cycle between node would actually give us the answer...if cycle is there then false else true.
Step 3: to detect cycle, visit every node one by one, and visited set is actually representing our current recursion stack - not all visited nodes ever, just the ones in the current path.\
Step 4: So after we finish exploring one route, we can remove the node before returning, because it might appear in another independent path later.
Step 5: If a node appears again while still in the recursion stack (visited), it means there's a cycle, else it's clean.


**Note: 
Time Complexity = O(V+E)
Space Complexity = O(V+E)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashSet< Integer> visited = new HashSet<>();
    HashMap< Integer, List< Integer >> map = new HashMap<>();
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        
        for(int i=0; i< numCourses; i++){
            map.put(i, new ArrayList<>());
        }

        for(int[] edge: prerequisites){
            map.get(edge[0]).add(edge[1]);
        }
        
        for(int mapValue=0; mapValue< numCourses; mapValue++){
            if(!dfs(mapValue)){
                return false;
            }
        }
        return true;
    }

    public boolean dfs(int mapValue){
        if(visited.contains(mapValue)){
            return false;
        }
        if(map.get(mapValue).isEmpty()){
            return true;
        }

        visited.add(mapValue);
        for(int nei: map.get(mapValue)){
            if(!dfs(nei)){
                return false;
            }
        }
        map.put(mapValue, new ArrayList<>());
        visited.remove(mapValue);
        return true;
    }
}
``` </pre>