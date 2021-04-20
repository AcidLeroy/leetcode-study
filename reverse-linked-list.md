# Reverse a linked list

As much as I thought this would be easy for me, it did take a bit of work. The reason for this is that any little mistake makes it hard to understand what happens. 
I managed to screw the answer up even after manually simulating each step, and it all boiled down to the fact that I didn't simulate the last step. 

In my first attempt, I did the iterative approach. There are a few things that helped me think about this problem. 

1) Don't start with the frist element, keep a `prev` element. This stratgy made it easier for me to think about because when I start focusing on the first element, I get stuck on the question "How do I get the second to last element to point to this one??" The easier answer: Don't worry about it yet. 
2) The next thing that I found helpful is to remember that you need a **temporary vairable** when you are doing the swap, otherwise you lose track of what the "next" item on the list should be. 

## Iterative solution

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    if (head === null) return null; 
    let last = head; 
    let prev = head; 
    let node = head.next; 
    last.next = null; 

    while(node !== null) {  
        let temp = node.next; // temp => 3, 4, 5, null
        node.next = prev;  // node.next => 1, 2, 3, 4
        prev = node;  // prev => 2, 3, 4, 5
        node = temp; // node = 3, 4, 5, null
    }
    
    
    return prev;
    
};
```


## Recursive solution

