<h3> Problem </h3>
Given the root of a binary tree, return true if it is a valid binary search tree, otherwise return false.

A valid binary search tree satisfies the following constraints:

The left subtree of every node contains only nodes with keys less than the node's key.
The right subtree of every node contains only nodes with keys greater than the node's key.
Both the left and right subtrees are also binary search trees.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/18f9a316-8dc2-4e11-d304-51204454ac00/public">
    Input: root = [2,1,3]
    Output: true
</pre>

Example 2:

<pre>

    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/6f14cb8d-efad-4221-2beb-fba2b19c8a00/public">
    Input: root = [1,2,3]
    Output: false

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  first thing to keep in mind is that, when we want to validate the tree, we have to do it recursively, it cannot be done just by comparing the the root node, or just it's parent node, it has to be validate in the whole tree, containing root and it's immediate or non-immediate parent nodes.
Step 2: that will make sure that it's validated through out.
Step 3: So to implement this logic, we can validate the tree by defining the range for example, the range of left sub tree should be within lowest possible number to the root value, and for right subtree, the range should be within root to maximum possible value. The range keeps changing as we traverse the tree deeply.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public boolean isValidBST(TreeNode root) {
        if(root == null){
            return true;
        }

        Queue< Object[] > queue = new LinkedList<>();
        queue.add(new Object[]{root, Long.MIN_VALUE, Long.MAX_VALUE});

        while(!queue.isEmpty()){
            Object[] current = queue.poll();
            TreeNode node = (TreeNode) current[0];
            long left = (long) current[1];
            long right = (long) current[2];

            if(!(left < node.val && right > node.val)){
                return false;
            }

            if(node.left != null){
                queue.add(new Object[]{node.left, left, (long) node.val});
            }

            if(node.right != null){
                queue.add(new Object[]{node.right, (long) node.val, right});
            }
        }
        return true;
    }
}
``` </pre>