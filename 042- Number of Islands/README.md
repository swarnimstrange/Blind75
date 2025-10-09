<h3> Problem </h3>
Given a 2D grid grid where '1' represents land and '0' represents water, count and return the number of islands.

An island is formed by connecting adjacent lands horizontally or vertically and is surrounded by water. You may assume water is surrounding the grid (i.e., all the edges are water).

Example 1:

<pre>
    Input: grid = [
    ["0","1","1","1","0"],
    ["0","1","0","1","0"],
    ["1","1","0","0","0"],
    ["0","0","0","0","0"]
    ]
    Output: 1
</pre>

Example 2:

<pre>
    Input: grid = [
    ["1","1","0","0","1"],
    ["1","1","0","0","1"],
    ["0","0","1","0","0"],
    ["0","0","0","1","1"]
    ]
    Output: 4

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: to find out number of islands we can go to every node in graph and check if it is a valid node for island.
Step 2: for it to be valid node of island it has to be under the contraint i.e 0 < r < ROWS and 0 < c < COLS, it should be equal to 1 and it should not have already visited.
Step 3: if the node passes all conditions meaning it is valid node to be traversed. so we can go ahead and check it neighbours for the same condition recursively and if valid mark it visited.
Step 4: the important thing to keep in mind is that we are not going to find multiple paths from same node, therefore there is no need to mark the latest node unvisited (every node should be visited).
Step 5: once it return true for the node, count the island and as one node can be visited only once, that basically means there's no way of returning count multiple times for multiple '1's.


**Note: 
Time Complexity = O(m*n)
Space Complexity = O(m*n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    int ROWS, COLS;
    boolean[][] visited;
    int maxCount = 0;
    public int numIslands(char[][] grid) {
        ROWS= grid.length; COLS = grid[0].length;
        visited = new boolean[ROWS][COLS];
        for(int r=0; r < ROWS; r++ ){
            for(int c=0; c < COLS; c++){
                if(dfs(r, c, grid)){
                    maxCount++;
                }
            }
        }
        return maxCount;
    }

    public boolean dfs(int r, int c, char[][] grid){
        if(r < 0 || r>=ROWS || c < 0 || c>=COLS
        || visited[r][c]
        || grid[r][c] != '1'){
            return false;
        }

        visited[r][c] = true;
        dfs(r+1, c, grid);
        dfs(r-1, c, grid);
        dfs(r, c+1, grid);
        dfs(r, c-1, grid);
        return true;
    }
}

``` </pre>