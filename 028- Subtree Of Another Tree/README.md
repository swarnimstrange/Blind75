<h3> Problem </h3>
Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/2991a77a-9664-46ed-528d-019e392f7400/public">
    Input: root = [1,2,3,4,5], subRoot = [2,4,5]
    Output: true
</pre>

Example 2:

<pre>

&nbsp;   Input: root = [1,2,3,4,5,null,null,6], subRoot = [2,4,5]

&nbsp;   Output: false

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To find if the binary tree contains subtree, we can traverse the root tree until we find the first node of Subtree.
Step 2: once we find the first node of subtree which is equal to actual root tree, we cann call the isSame() function on it.
Step 3: one thing to keep in mind is that, even if the tree is present in either of the left subtree or right subtree it should return true in that case.

**Note: 
Time Complexity = O(m*n)
Space Complexity = O(m+n)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {  
    public boolean isSubtree(TreeNode root, TreeNode subRoot) {
        if(root == null){
            return false;
        }

        if(isSameTree(root, subRoot)){
            return true;
        }

        return isSubtree(root.left, subRoot) || isSubtree(root.right, subRoot);

    }

    public boolean isSameTree(TreeNode root, TreeNode subRoot) {
        if(root == null && subRoot == null){
            return true;
        }

        if((root == null && subRoot != null) || (root != null && subRoot == null)){
            return false;
        }

        if(root.val != subRoot.val){
            return false;
        }

        return isSameTree(root.left, subRoot.left) && isSameTree(root.right, subRoot.right);

    }

}
``` </pre>