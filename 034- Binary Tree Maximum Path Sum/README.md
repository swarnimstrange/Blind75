<h3> Problem </h3>
Given the root of a non-empty binary tree, return the maximum path sum of any non-empty path.

A path in a binary tree is a sequence of nodes where each pair of adjacent nodes has an edge connecting them. A node can not appear in the sequence more than once. The path does not necessarily need to include the root.

The path sum of a path is the sum of the node's values in the path.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/9896b041-9021-44c2-ab3e-5cff76adf100/public">
    Input: root = [1,2,3]
    Output: 6
</pre>

Example 2:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/19ce1187-387e-4323-f2c9-1a317ab36200/public">
    Input: root = [-15,10,20,null,null,15,5,-5]
    Output: 40
</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To solve this problem, we need to keep in mind that sum of any node is equal to sum of it's left nodes, right nodes and root node.
Step 2: so, to get the maximum sum of a path, we can find the maximum sum of all nodes available, then return the maximum sum.
Step 3: but the problem with this approach could be that, we might get negative values as well, which could lower the sum, to tackle this problem, get the sum only when value is in positive or else get 0 as sum, so that it will not lower the total sum.
Step 4: one more trick to keep in mind is that, when taking routes of tree node, we can either take left or right, taking both routes will not be a path but a multiple path intersection, so take the maximum value between left and right could give us maximum path.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    int max = 0;
    public int maxPathSum(TreeNode root) {
        int maxi = findMaximumPath(root);
        return max;
    }

    public int findMaximumPath(TreeNode root){
        if(root == null){
            return 0;
        }

        int left = Math.max(0, findMaximumPath(root.left));
        int right = Math.max(0, findMaximumPath(root.right));

        max = Math.max(max,root.val + left + right);
        return root.val + Math.max(left, right);
    }
}
``` </pre>