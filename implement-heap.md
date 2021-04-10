# Implement a heap

There are probably many ways to do this, but I chose to use the common way which is to back the heap with an array. The nice thing about this 
way of doing it, is that you can always push elements to the end of the array when inserting, then "bubble" the answer to the top. There were a 
few concepts that I struggled with on this problem. 

1) Indexing - part of the secret to implementing a heap correctly using an array is to make sure you get the indexing correct. Namely, we need to
   to have methods that get parent, left and right child, and the determination if the node is a leaf node or not. 
2) Bubbling up/down - You need both of these in order to implement the heap. The reason is that when you add a new node, you need to bubble that answer up. When you remove a node, you need to 
   bubble that answer down. Bubbling up is much easier to implement because we only need to be concerned with the parent. Bubbling down is more difficult because we need to 
   check which node is great, the right or the left, or if there is even a right node. 
   
   **note** order of the left and right nodes does not matter regardless of whether it is a min/max heap. I.e. the left node can be great, equal, or less than the right node to 
   satisfy the heap property. 
   
   Below is my code with a few tests 
   
   
```js

class Heap {
    constructor (comp){
        this.comp = comp; 
        this.heap = []; 
    }

    parent(i){
        if (i <= 0) return -1; 
        return Math.floor((i-1)/2);  
    }

    leftChild(i){
        return i*2 + 1; 
    }

    rightChild(i){
        return 2 * (i + 1); 
    }

    isLeaf(i) {
        return this.leftChild(i) > this.heap.length; 
    }

    root() {
        return this.heap[0]; 
    }

    swap(posA, posB) {
        const temp = this.heap[posA]; 
        this.heap[posA] = this.heap[posB]; 
        this.heap[posB] = temp;
    }

    insert(val) {
        this.heap.push(val); 
        let currPos = this.heap.length - 1; 
        // comp = greaterThan == max heap
        // Check if parent is greater/less than and not the root (exit when we swap the root)
        while (this.comp(this.heap[currPos], this.heap[this.parent(currPos)]) && currPos > 0){
            this.swap(currPos, this.parent(currPos)); 
            currPos = this.parent(currPos); 
        } 
    }

    // Remove element at location i. 
    remove(i){
        if (this.heap.length == 1){
            this.heap = []; 
            return; 
        }
        const last = this.heap.pop(); 
        this.heap[i] = last; 
        this.heapify(i); 
    }

    heapify(i) {
        // console.log('heapify  = ' + i + ' heap = ' + this.heap); 

        if (!this.isLeaf(i)){
            // greater than example
            // if left child of current is greater than current, we should swap 

            // Check to see if we have a right node
            if (this.rightChild(i) < this.heap.length) {
                // is left greater than right? 
                if (this.comp(this.heap[this.leftChild(i)], this.heap[this.rightChild(i)])){
                   
                    if (this.comp(this.heap[this.leftChild(i)], this.heap[i])){
                        this.swap(this.leftChild(i), i); 
                        this.heapify(this.leftChild(i)); 
                    }
                    // Otherwise, things are in order and we can stop recursing
                } else {
                    if (this.comp(this.heap[this.rightChild(i)], this.heap[i])){
                        this.swap(this.rightChild(i), i); 
                        this.heapify(this.rightChild(i)); 
                    }
                }
            // Proceed with only logic of left node. 
            } else {
                if (this.comp(this.heap[this.leftChild(i)], this.heap[i])){
                    this.swap(this.leftChild(i), i); 
                    this.heapify(this.leftChild(i)); 
                }
            }

        }
    }
}

function greaterThan(a, b) {
    return a > b; 
}

function lessThan(a, b) {
    return a < b; 
}


function testHeap() {
    let maxHeap = new Heap(greaterThan); 
    maxHeap.insert(100); 
    maxHeap.insert(1); 
    maxHeap.insert(2); 
    if (maxHeap.root() !== 100){
        throw "Expected root to be 100, but got " + maxHeap.root() + " instead"; 
    }

    maxHeap.insert(101); 
    if (maxHeap.root() !== 101){
        throw "Expected root to be 101, but got " + maxHeap.root() + " instead"; 
    }

    console.log('heap = ', maxHeap.heap); 
    
    maxHeap.remove(0); 

    console.log('heap = ', maxHeap.heap); 

    if (maxHeap.root() !== 100) {
        console.log('heap = ', maxHeap.heap); 
        throw "Failed to extract the right element."
    }

    maxHeap.insert(3); 
    maxHeap.insert(4); 
    maxHeap.insert(5); 
    console.log('heap5 = ', maxHeap.heap); 

    if (maxHeap.root() !== 100) {
        console.log('heap = ', maxHeap.heap); 
        throw "Root should be 100, but got " + maxHeap.root() + " instead!"
    }

    console.log("removing 100...."); 

    maxHeap.remove(0); 

    if (maxHeap.root() !== 5) {
        console.log('heap = ', maxHeap.heap); 
        throw "Root should be 5, but got " + maxHeap.root() + " instead!"
    }
    console.log('heap = ', maxHeap.heap); 
    maxHeap.remove(0); 
    maxHeap.remove(0); 

    if (maxHeap.root() !== 3){
        console.error("heap = ", maxHeap.heap); 
        throw "Root should be 3, but got " + maxHeap.root() + " instead!"; 
    }
    maxHeap.remove(0); 
    if (maxHeap.root() !== 2){
        console.error("heap = ", maxHeap.heap); 
        throw "Root should be 2, but got " + maxHeap.root() + " instead!"; 
    }
    console.log('heap = ', maxHeap.heap); 

    maxHeap.remove(0)
    console.log('After removing root: heap = ', maxHeap.heap); 

    if (maxHeap.root() !== 1){
        console.error("heap = ", maxHeap.heap); 
        throw "Root should be 1, but got " + maxHeap.root() + " instead!"; 
    }

    maxHeap.remove(0); 
    console.log('After removing all elements: heap = ', maxHeap.heap); 
    console.log('Success!'); 
}

testHeap(); 
```
