<h3> Problem </h3>
Given the root of a binary tree, return its depth.

The depth of a binary tree is defined as the number of nodes along the longest path from the root node down to the farthest leaf node.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/5ea6da77-7e43-43e0-dd9d-e879ca0b1600/public">
    Input: root = [1,2,3,null,null,4]
    Output: 3
</pre>

Example 2:

<pre>

&nbsp;   Input: root = []

&nbsp;   Output: 0

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To find the binary tree depth, we'll keep this logic in mind that if any of the child is present for a root node, then that increases the depth.
Step 2: if both left and right nodes are present then also the depth will increase by 1, if any of then left or right is present then also the depth will increase by 1. 
Step 3: if both left and right are not present then that means the depth will not increase it will return 0.
Step 4: keeping the same logic in ming we can recursively call all the node, then compare the maximum depth of left side with right side then return the maximum result.

**Note: 
Time Complexity = O(n)
Space Complexity = O(n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    int maxCount = 0;
    public int maxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        return (Math.max(maxDepth(root.left), maxDepth(root.right)) + 1);
    }
}
``` </pre>