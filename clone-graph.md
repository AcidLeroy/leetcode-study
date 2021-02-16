# Clone Graph

This problem can be solved using two techniques: depth first search and breadth first search. 

## Breadth first search

Here is my solution for the Breadth First Search

```java 
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null; 
        // This is the queue used to keep track of the nodes that need to be visited. 
        Queue<Node> q = new LinkedList<Node>(); 
        // This hashmap maps originalNode -> copyNode. 
        // This is necessary so we can reference the current node and its copy.
        // Details below
        HashMap<Node, Node> copies = new HashMap<Node, Node>(); 
        
        // Add the root node to the queue
        q.add(node);
        // Create a copy of the node. Notice that we don't include the neighbors
        Node rootCopy = new Node(node.val); 
        // Initialize the mapping
        copies.put(node, rootCopy); 
        
        while(q.size() > 0) {
            // Remove the first node from the queue
            Node curr = q.remove(); 
            // Iterate over all the neighbors
            for (Node n : curr.neighbors){
                // If the neighbor isn't in the map yet, we need to create it
                if (!copies.containsKey(n) ) {
                    // Add this neighbor to queu
                    q.add(n); 
                    // Initialize it
                    copies.put(n, new Node(n.val)); 
                }
                // Get the copy
                Node c = copies.get(curr); 
                // Add the neighbors
                c.neighbors.add(copies.get(n)); 
            }
           
        }
        return rootCopy; 
    }
}
```

## Depth first search
This code is basically identical, other than it uses a stack instead of a queue
```java
class Solution {
    public Node cloneGraph(Node node) {
        if (node == null) return null; 
        Deque<Node> stack = new LinkedList<Node>(); 
        HashMap<Node, Node> copies = new HashMap<Node, Node>(); 
        
        stack.addFirst(node);
        Node rootCopy = new Node(node.val); 
        copies.put(node, rootCopy); 
        
        while(stack.size() > 0) {
            Node curr = stack.removeFirst(); 
            for (Node neighbor : curr.neighbors){
                if (!copies.containsKey(neighbor)){
                    // Neighbor hasn't been visited
                    stack.addFirst(neighbor); 
                    copies.put(neighbor, new Node(neighbor.val)); 
                }
                copies.get(curr).neighbors.add(copies.get(neighbor)); 
            }
        }
        
        return rootCopy; 
    }
}
```
