# Course Schedule

This problem caused me many problems initially. I believe it did so because I spent too much time thinking about course dependencies and not 
initially recognizing that it was a simple cycle detection problem in a directed graph. 

Once I realized this, the algorithm became much easier to develop. I followed these steps to come up with the algorithm. 

```
                        (1) Visit a Node
                               |
                               | 
                        (2) Is Node in PROCESSING state? 
                               |     \
                               |      \
                               NO      YES -------- Exit - we found a cycle
                               |
                               |
                        (3) Can I take this
                             class? 
                             /    \
                            /      \
                           YES      \
                           |        NO  ------- (4) Mark node as PROCESSING and visit prerequisites (recurse)
                           | 
                      (4) Mark Node as
                      processed

```

## Solution

```javascript
const NodeState = {
    UNPROCESSED: 0, 
    PROCESSED: 1, 
    PROCESSING: 2
}

function containsCycle(currentCourse, preReqMap, nodeState){
    if (nodeState[currentCourse] === NodeState.PROCESSING) return true; 
    
    if (nodeState[currentCourse] === NodeState.PROCESSED) return false; 
    
    nodeState[currentCourse] = NodeState.PROCESSING; 
    
    const preReqs = preReqMap[currentCourse]; 
    if (!preReqs){
        nodeState[currentCourse] = NodeState.PROCESSED; 
        return false; 
    }
    for (let i = 0; i < preReqs.length; i++){
        if (containsCycle(preReqs[i], preReqMap, nodeState)) return true; 
    }
    
    nodeState[currentCourse] = NodeState.PROCESSED; 
    return false; 
}

/**
 * @param {number} numCourses
 * @param {number[][]} prerequisites
 * @return {boolean}
 */
var canFinish = function(numCourses, prerequisites) {
    
    let preReqMap = {}; 
    
    for (let i = 0; i < prerequisites.length; i++) {
        const course = prerequisites[i][0]; 
        const prereq =  prerequisites[i][1];
        if (preReqMap[course]) {
            preReqMap[course].push(prereq); 
        } else {
            preReqMap[course] = [prereq]
        }
    }
    
    let nodeState = {}; 
    for (let i = 0; i < numCourses; i++) {
        nodeState[i] = NodeState.UNPROCESSED
    }
    
    
    for (let currentCourse = 0; currentCourse < numCourses; currentCourse++){
        if (containsCycle(currentCourse, preReqMap, nodeState)) return false; 
    }
    
    return true; 
   
};
```
