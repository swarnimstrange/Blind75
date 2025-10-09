<h3> Problem </h3>
Given a binary tree where all node values are unique, and two nodes from the tree p and q, return the lowest common ancestor (LCA) of the two nodes.

The lowest common ancestor between two nodes p and q is the lowest node in a tree T such that both p and q as descendants. The ancestor is allowed to be a descendant of itself.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/2080ee6a-3d27-4cd5-0db2-07672ead8200/public">
    Input: root = [5,3,8,1,4,7,9,null,2], p = 3, q = 8
    Output: 5
</pre>

Example 2:

<pre>

&nbsp;   Input: root = [5,3,8,1,4,7,9,null,2], p = 3, q = 4

&nbsp;   Output: 3

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To find lowest common ancestor in Binary Tree,  we can check if any one of the both values are equal to root, if yes, return the root.
Step 2: then we can traverse in left subtree first and just when we get the first element, return that element as node. no need to check for the second value in the same left subtree again.
Step 3: then traverse the right sub tree and check if the other element is available in that
    if available -: then it means both values are in different subtree, hence return root.
    if not available -: then it means, the value must be beneath the first element of left subtree, hence return the element we took as node from left subtree.
Step 4: if we did not find any value in left subtree. then traverse the right sub tree and return the element.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null){
            return null;
        }

        if(root.val == p.val || root.val == q.val){
            return root;
        }

        TreeNode leftLCA = lowestCommonAncestor(root.left, p, q);
        TreeNode rightLCA = lowestCommonAncestor(root.right, p, q);


        if(leftLCA != null && rightLCA != null){
            return root;
        }
        else if(leftLCA != null){
            return leftLCA;
        }
        else{
            return rightLCA;
        }
        
    }
}
``` </pre>