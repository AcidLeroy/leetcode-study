# Subtree of another tree

This problem was rated as easy but I struggled with it because I made a simple mistake in my recursive calls. I got by initially by thinking that it was correct because
I was only checking to see if the first three nodes of the tree were equal, not all of them. I'll demonstrate in my solution below: 

## Solution
```java
class Solution {
    private Boolean foundSubtree = false; 
    public boolean isEqual(TreeNode s, TreeNode t) {
        if (s == null && t == null) return true; 
        if (s == null || t == null) return false; 
        
        boolean left = isEqual(s.left, t.left); 
        boolean right = isEqual(s.right, t.right);
        
        return (s.val == t.val) && left && right; 
        
    }
    
    public void subTree(TreeNode s, TreeNode t) {
        if (this.foundSubtree) return; 
        if (s == null) return; 
        
        if (isEqual(s, t)){
            // System.out.println("Found subtree---"); 
            this.foundSubtree = true; 
            return; 
        }
        // THE ISSUE
        // Below is the correct implementation; however, I had originally put `isEqual` for both left and the right there. 
        // The issue is that I didn't continue recursing through the tree, so I passed the initial tets on leetcode, 
        // but then started failing as the test cases became more complex.
        subTree(s.right, t); 
        subTree(s.left, t); 
       
        return; 
    }
    
    public boolean isSubtree(TreeNode s, TreeNode t) {
        this.foundSubtree = false; 
        subTree(s, t); 
        // System.out.println("Found subtree: "+ this.foundSubtree); 
        return foundSubtree; 
    }
}
```
