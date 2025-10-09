<h3> Problem </h3>
A prefix tree (also known as a trie) is a tree data structure used to efficiently store and retrieve keys in a set of strings. Some applications of this data structure include auto-complete and spell checker systems.

Implement the PrefixTree class:

PrefixTree() Initializes the prefix tree object.
void insert(String word) Inserts the string word into the prefix tree.
boolean search(String word) Returns true if the string word is in the prefix tree (i.e., was inserted before), and false otherwise.
boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.

Example 1:

<pre>
    Input: 
    ["Trie", "insert", "dog", "search", "dog", "search", "do", "startsWith", "do", "insert", "do", "search", "do"]

    Output:
    [null, null, true, false, true, null, true]

    Explanation:
    PrefixTree prefixTree = new PrefixTree();
    prefixTree.insert("dog");
    prefixTree.search("dog");    // return true
    prefixTree.search("do");     // return false
    prefixTree.startsWith("do"); // return true
    prefixTree.insert("do");
    prefixTree.search("do");     // return true

</pre>

<h3> Algorithm </h3>

<pre>

Step 1: To solve this problem, think of this as tree where one node of char is connected to another char, at last forming the word.
Step 2: So basically, a node in this tree would contain the next node whereabouts and to denote if the word is completed, a boolean to denote the end of the word.
Step 3: keep in mind that everytime we are traversing the node, to get the next char node, we have to make the current node equal to the next node like we do in linked list and tree.
Step 4: Insert every charater one by one in the tree, and if the node for that is not available then create the node and then assign the new char to it. seacrh will be same as insert just instead of inserting when we did not find the char, we will have to return false and if end of the word does not matches then also we will have to return false


**Note: 
Time Complexity = O(n) (n is size of word)
Space Complexity = O(t) (t is total number of nodes created in the Trie)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class TrieNode{
    TrieNode[] children = new TrieNode[26];
    boolean endOfWord = false;
}

class PrefixTree {
    TrieNode root;

    public PrefixTree() {
        root = new TrieNode();
    }

    public void insert(String word) {
        TrieNode curr = root;
        for(int i=0; i< word.length(); i++){
            char c = word.charAt(i);
            int cPos = c - 'a';
            if(curr.children[cPos] == null){
                curr.children[cPos] = new TrieNode();
            }
            curr = curr.children[cPos];
        }
        curr.endOfWord = true;
    }

    public boolean search(String word) {
        TrieNode curr = root;
        for(int i=0; i< word.length(); i++){
            char c = word.charAt(i);
            int cPos = c - 'a';
            if(curr.children[cPos] == null){
                return false;
            }
            curr = curr.children[cPos];
        }
        if(curr.endOfWord != true){
            return false;
        }
        return true;
    }

    public boolean startsWith(String prefix) {
        TrieNode curr = root;
        for(int i=0; i< prefix.length(); i++){
            char c = prefix.charAt(i);
            int cPos = c - 'a';
            if(curr.children[cPos] == null){
                return false;
            }
            curr = curr.children[cPos];
        }
        return true;
    }
}
``` </pre>