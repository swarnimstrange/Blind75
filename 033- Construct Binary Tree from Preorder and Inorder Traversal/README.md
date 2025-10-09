<h3> Problem </h3>
You are given two integer arrays preorder and inorder.

preorder is the preorder traversal of a binary tree
inorder is the inorder traversal of the same tree
Both arrays are of the same size and consist of unique values.
Rebuild the binary tree from the preorder and inorder traversals and return its root.

Example 1:

<pre>
    <img alt="" src="https://imagedelivery.net/CLfkmk9Wzy8_9HRyug4EVA/938c14d3-6669-47ab-924b-a1a08640f200/public">
    Input: preorder = [1,2,3,4], inorder = [2,1,3,4]
    Output: [1,2,3,null,null,null,4]
</pre>

Example 2:

<pre>
    Input: preorder = [1], inorder = [1]
    Output: [1]

</pre>


<h3> Algorithm </h3>

<pre>

Step 1:  To solve this problem, we need to keep in mind that preorder will always have root before left and right nodes, and for inorder traversal, root will be between left and right nodes.
Step 2: so, to form a tree, keep going forward in preorder list, and the first node we find must me the root, so look for the root in inorder list.
Step 3: when we find the index at which the root is present in inorder list, that means the elements left to it must be in the left tree and right to it must be in the right tree.
Step 4: Form a tree based on that, and keep traversing the preorder index and keep finding that node in inorder list until we find nothing.

**Note: 
Time Complexity = O(n) (n is no of nodes of tree)
Space Complexity = O(n) 
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class Solution {
    HashMap< Integer, Integer > map = new HashMap<>();
    int preOrderIndex = 0;
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        for(int i=0; i < inorder.length; i++){
            map.put(inorder[i], i);
        }
        return build(preorder, 0, preorder.length-1);
    }

    public TreeNode build(int[] preorder, int l, int r){
        if(l > r){
            return null;
        }
        TreeNode root = new TreeNode(preorder[preOrderIndex]);
        preOrderIndex++;
        int getInOrIndex = map.get(root.val);
        TreeNode left = build(preorder, l, getInOrIndex-1);
        TreeNode right = build(preorder, getInOrIndex+1, r);

        root.left = left;
        root.right = right;
        return root;
    }
}
``` </pre>