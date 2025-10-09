<h3> Problem </h3>
Given a binary search tree (BST) where all node values are unique, and two nodes from the tree p and q, return the lowest common ancestor (LCA) of the two nodes.

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

Step 1:  To find lowest common ancestor in BST,  we can check if both the values belong in left, if yes then we call recurcively same function with left subtree.
Step 2: we can check if both the values belong in right, if yes then we call recurcively same function with right subtree.
Step 3: one thing to keep in mind is that, whenever any of the value becomes equal to the root, we have to return the root immediately. Step 4: And if one value belong in left subtree and another value belongs in right subtree, then also we have to return root immediately.

**Note: 
Time Complexity = O(h) (h is height of tree)
Space Complexity = O(h) (h is height of tree)
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
        
        if(p.val>root.val && q.val > root.val){
            return lowestCommonAncestor(root.right, p ,q);
        }
        else if(p.val < root.val && q.val < root.val){
            return lowestCommonAncestor(root.left, p ,q);
        }
        else{
            return root;
        }
        
    }
}
``` </pre>