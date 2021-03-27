# Implement a Trie

This problem was actually pretty fun. One of the first mistakes I made though, was that I used a linked list to hold the "neighbors" for each node. This meant that I had to traverse
all the neighbors O(N) time for each lookup. After changing my solution to use a HashMap, the performance of my program was much better: both in time and space complexity. Another issue
that I oringally had was that I did not account for the difference between a prefix and a "whole word". As a result, I had to add another field to my object for 
keeping track of when an "ending" was encountered. Hence the in the TrieNode, we have a boolean `end` field. 
My solution is below: 

## Solution
```java

class TrieNode {
    public Character val; 
    public Boolean end; 
    public HashMap<Character, TrieNode> neighbors; 
    public TrieNode() {
        this.val = null; 
        this.end = false; 
        this.neighbors = new HashMap<Character, TrieNode>(); 
    }
    
    public TrieNode(Character val) {
        this.val = val; 
        this.end = false; 
        this.neighbors = new HashMap<Character, TrieNode>(); 
    }
    
}

class Trie {

    TrieNode root; 
    /** Initialize your data structure here. */
    public Trie() {
       this.root = new TrieNode();  
    }
    
    
    private void insertHelper(TrieNode root, String word) {
        if (word.length() == 0 )  return; 
        if (word == null) return; 
        if (root == null) return; 
        // System.out.println("word = "+ word); 
        String sub = word.substring(1, word.length()); 

        Character c = word.charAt(0); 
        if (root.neighbors.containsKey(c)){
            TrieNode n = root.neighbors.get(c); 
            // last character? 
            if (word.length() == 1) n.end = true; 
            // Have a match, add the rest
            insertHelper(n, sub);  
        } else {
            // If we make it here, we don't have the starting prefix,
            // so we add it. 
            TrieNode newRootPrefix = new TrieNode(c);
            if (word.length() == 1) {
                // System.out.println("At the end " + word.charAt(0)); 
                newRootPrefix.end = true; 
            }
            root.neighbors.put(c, newRootPrefix); 
            insertHelper(newRootPrefix, sub); 
        }
         
       
    }
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        insertHelper(this.root, word);  
    }
    
    public boolean searchHelper(TrieNode root, String word) {
        if (root == null) return false; 
    
        if (word.length() == 0 && root.end) return true; 
        if (word.length() == 0) return false; 
        
        Character c = word.charAt(0); 
        if (root.neighbors.containsKey(c)) {
            String sub = word.substring(1, word.length()); 
            return searchHelper(root.neighbors.get(c), sub); 
        } else {
            return false;
        }
         
    } 
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        return searchHelper(this.root, word); 
    }
    
     public boolean startsWithHelper(TrieNode root, String word) {
         // System.out.println("starts with = " + word); 
        if (word.length() == 0) return true; 
        
        Character c = word.charAt(0); 
        if (root.neighbors.containsKey(c)) {
            String sub = word.substring(1, word.length()); 
            return startsWithHelper(root.neighbors.get(c), sub); 
        } else {
           return false;  
        }
         
        
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        return startsWithHelper(this.root, prefix); 
    }
}

/**
 * Your Trie object will be instantiated and called as such:
 * Trie obj = new Trie();
 * obj.insert(word);
 * boolean param_2 = obj.search(word);
 * boolean param_3 = obj.startsWith(prefix);
 */
```
