<h3> Problem </h3>
You are given a rectangular island heights where heights[r][c] represents the height above sea level of the cell at coordinate (r, c).

The islands borders the Pacific Ocean from the top and left sides, and borders the Atlantic Ocean from the bottom and right sides.

Water can flow in four directions (up, down, left, or right) from a cell to a neighboring cell with height equal or lower. Water can also flow into the ocean from cells adjacent to the ocean.

Find all cells where water can flow from that cell to both the Pacific and Atlantic oceans. Return it as a 2D list where each element is a list [r, c] representing the row and column of the cell. You may return the answer in any order.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/3899fae1-ab18-4d6b-15b4-c7f7aa224700/public">
    Input: heights = [
    [4,2,7,3,4],
    [7,4,6,4,7],
    [6,3,5,3,6]
    ]

    Output: [[0,2],[0,4],[1,0],[1,1],[1,2],[1,3],[1,4],[2,0]]

</pre>

Example 2:

<pre>
    Input: heights = [[1],[1]]

    Output: [[0,0],[0,1]]

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: One thing to keep in mind before solving this problem is that, instead of going for all nodes to the corner nodes, we can go from corner node to the nodes which are greater than it's previous node (as the water will travel from higher to lower until it reaches the corner node, we can take the opposite scenario where we can start from corner node traverse to higher node).
Step 2: As we are starting from corner nodes, we can traverse for all four directions and try to find the higher node if found mark it visited (if it is traversed from pacific ocean corner, mark it in pacific set or if it is traversed from atlantic ocean corner, mark it in atlantic set).
Step 3: At last once we have visited all nodes, we can traverse all nodes and check if that is visited in both pacific and atlantic, then add it in the result set.
Step 4: once we check all the nodes, return the common cells list.


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
    public List< List< Integer >> pacificAtlantic(int[][] heights) {
        List< List < Integer >> res = new ArrayList<>();
        ROWS = heights.length; COLS = heights[0].length;
        boolean[][] pacVisited = new boolean[ROWS][COLS]; 
        boolean[][] atlVisited = new boolean[ROWS][COLS];

        for(int c=0; c < COLS; c++){
            dfs(0, c, pacVisited, heights[0][c], heights);
            dfs(ROWS-1, c, atlVisited, heights[ROWS-1][c], heights);
        }

        for(int r=0; r < ROWS; r++){
            dfs(r, 0, pacVisited, heights[r][0], heights);
            dfs(r, COLS-1, atlVisited, heights[r][COLS-1], heights);
        }

        for(int r=0; r < ROWS; r++){
            for(int c=0; c < COLS; c++){
                if(pacVisited[r][c] && atlVisited[r][c]){
                    res.add(List.of(r,c));
                }
            }
        }

        return res;
    }

    public void dfs(int r, int c, boolean[][] visited, int prevHeight, int[][] heights){
        if(r < 0 || r>=ROWS || c< 0 || c>=COLS
        || visited[r][c]
        || heights[r][c] < prevHeight){
            return;
        }

        visited[r][c] = true;
        dfs(r+1, c, visited, heights[r][c], heights);
        dfs(r-1, c, visited, heights[r][c], heights);
        dfs(r, c+1, visited, heights[r][c], heights);
        dfs(r, c-1, visited, heights[r][c], heights);
    }
}
``` </pre>