<h3> Problem </h3>
Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) in the tree.

A binary search tree satisfies the following constraints:

The left subtree of every node contains only nodes with keys less than the node's key.
The right subtree of every node contains only nodes with keys greater than the node's key.
Both the left and right subtrees are also binary search trees.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/02eca3db-f72f-4277-7134-faec4f02e500/public">
    Input: root = [2,1,3], k = 1
    Output: 1
</pre>

Example 2:

<pre>

    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/dca6c42d-2327-4036-f7f2-3e99d8203100/public">
    Input: root = [4,3,5,2,null], k = 4
    Output: 5

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To solve this problem, we need to know Inorder Traversal, which start from left -> root -> right
Step 2: the lowest element will be the left most element, and the second lowest will be it's immediated parent root and so on
Step 3: So it can be implemented using Inorder Travesal where we can store every sequence with node value in a map, then at last just return the k value from that Map.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashMap< Integer, Integer > numMap = new HashMap<>();
    int l = 1;
    public int kthSmallest(TreeNode root, int k) {
       checKElement(root);
       return numMap.get(k);
    }

    TreeNode checKElement(TreeNode root) {
        if(root == null){
            return null;
        }
        checKElement(root.left);
        numMap.put(l++,root.val);
        checKElement(root.right);
        return root;
    }
}
``` </pre>