<h3> Problem </h3>
Given a 2-D grid of characters board and a string word, return true if the word is present in the grid, otherwise return false.

For the word to be present it must be possible to form it with a path in the board with horizontally or vertically neighboring cells. The same cell may not be used more than once in a word.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/7c1fcf82-71c8-4750-3ddd-4ab6a666a500/public">
    Input: 
    board = [
    ["A","B","C","D"],
    ["S","A","A","T"],
    ["A","C","A","E"]
    ],
    word = "CAT"

    Output: true
</pre>

<h3> Algorithm </h3>

<pre>

Step 1: To solve this problem, think of this problem as decision tree approach of four ways.
Step 2: Where we have to backtrack to find every combination that can return the word search.
Step 3: we have to go to every node and try traversing from that location to find the word. the traversing can happen in four ways (as diagonals are not considered). the four ways can be up (r+1), down (r-1), right (c+1) and left (c-1)
Step 4: the base condiiton for returning will be that -:
        1 -: when we reach the solution. i.e the index is equal to word length then return true, (one doubt can be that if we are returning true just when we find the length then why are we not returning when we get "caa" not "cat". that's because we are only traversing the index length we find the combination. for example when we find "ca" then our index = 1, when we find "cat" then our index = 2, therefore we have found our word, then whenever we go for traversing further then only we can return true, becuase we found the word).
        2 -: when the row or column goes outbound i.e r < 0 or r > rows or c < 0 or c > cols, then return false
        3 -: when character at board is not equal to charater at index of word, then return false.
        4 -: when character at board is already in visited, then return false.
Step 5: once we return to function, that means either we found the word, or we have gone out of choice or bound. that means we will remove the last element from visited set and return.


**Note: 
Time Complexity = O(m * (4^n)) (m is r*c, n is size of word)
Space Complexity = O(n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    boolean[][] visited;
    int ROWS; int COLS;
    public boolean exist(char[][] board, String word) {
        ROWS = board.length;
        COLS = board[0].length;
        visited = new boolean[ROWS][COLS];
        for(int r=0; r < ROWS ; r++){
            for(int c=0; c < COLS ; c++){
                if(dfs(r, c, board, word, 0)){
                    return true;
                }
            }
        }
        return false;
    }

    boolean dfs(int r, int c, char[][] board, String word, int index){
        if( index == word.length() ){
            return true;
        }

        if(r < 0 || r >= ROWS
        || c < 0 || c>=COLS
        || word.charAt(index) != board[r][c]
        || visited[r][c]){
            return false;
        }

        visited[r][c] = true;
        boolean res = dfs(r+1, c, board, word, index+1)||
        dfs(r-1, c, board, word, index+1)||
        dfs(r, c+1, board, word, index+1)||
        dfs(r, c-1, board, word, index+1);
        visited[r][c] = false;
        return res;
    }

}
``` </pre>