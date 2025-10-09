<h3> Problem </h3>
Design a data structure that supports adding new words and searching for existing words.

Implement the WordDictionary class:

void addWord(word) Adds word to the data structure.
bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.

Example 1:

<pre>
    Input:
    ["WordDictionary", "addWord", "day", "addWord", "bay", "addWord", "may", "search", "say", "search", "day", "search", ".ay", "search", "b.."]

    Output:
    [null, null, null, null, false, true, true, true]

    Explanation:
    WordDictionary wordDictionary = new WordDictionary();
    wordDictionary.addWord("day");
    wordDictionary.addWord("bay");
    wordDictionary.addWord("may");
    wordDictionary.search("say"); // return false
    wordDictionary.search("day"); // return true
    wordDictionary.search(".ay"); // return true
    wordDictionary.search("b.."); // return true


</pre>

<h3> Algorithm </h3>

<pre>

Step 1: addWord is simple, put the charaters one by one in the trie node and then traverse the trieNode to the current added node.
Step 2: but the problem is there in search as, we want to get the search right along with '.'
Step 3: but before solving this keep in mind that whenever if find '.' that mean we have no way other than checking all node present in current node.
Step 4: One common mistake we do is that once we find the '.' we run for loop for checking all element for the character, but do not increment the character, which is wrong for example -: if we have dog in trienode and we are searching for '.o.', when we encounter '.' traverse all the node present currently which might contain next character. so increment the character, put the current node as the one in for loop and run the dfs for current character, repeat this until loop is over then return true;
Step 5: Another common mistake is that, we do not check for length when we are encountering dots. for example -: if we have 'dog' in our trie and search is for 'do..', in this case it'll should return false. so keep in mind that even when the loop is in progress but we got all current nodes to be null (that is the case for 4th character i.e 'g' node in dog has no children (children[] is all null)) we should return false.


**Note: 
Time Complexity = O(n) (n is size of word)
Space Complexity = O(n+t) (t is total number of nodes created in the Trie)
**

</pre>

<h3> Code in Java </h3>

<pre>
```java
class TrieNode{
    TrieNode[] children = new TrieNode[26]; 
    boolean endOfWord = false;
}

class WordDictionary {
    TrieNode root;

    public WordDictionary() {
        root = new TrieNode();
    }

    public void addWord(String word) {
        TrieNode cur = root;
        for(int i = 0; i < word.length(); i++){
            int c = word.charAt(i) - 'a';
            if(cur.children[c] == null){
                cur.children[c] = new TrieNode();
            }
            cur = cur.children[c];
        }
        cur.endOfWord = true;
    }

    public boolean search(String word) {
        return dfs(word, 0, root);
    }
        
    public boolean dfs(String word, int index, TrieNode root) {
        TrieNode cur = root;
        
        for(int i = index; i < word.length(); i++){
            char c = word.charAt(i);
            if(c == '.'){
                for(TrieNode child: cur.children){
                    if(child != null && dfs(word, i+1, child)){
                        return true;
                    }
                }
                return false;
            }
            else{
                if(cur.children[c-'a'] == null){
                    return false;
                }
                cur = cur.children[c-'a'];
            }
        }
        if(cur.endOfWord){
            return true;
        }
        else{
            return false;
        }
    }
}
``` </pre>