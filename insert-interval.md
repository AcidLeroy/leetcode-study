# Insert Intervals

This problem proved to be a bit of a challenge for me based on some of the ways I think through problems like this. 
One issue I have is that this problem makes it so I end up getting tangled in nested `if/else` statements. 
The key to solving this problem is to make sure that you draw out the solution and also noting that the
answer does not have to sorted. In one of the first attempts at writing this code, I attempted to add the 
item "inline" in them merged list. Though I think this is possible, it makes the code much more difficult to follow. 
So the best solution I found for me, was to break the problem into two cases: cases where the interval overlaps the current list, and cases where it does not.

## Solution
```java
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> result = new ArrayList<int[]>(); 
        for(int[] in: intervals){
          // The right most point does not overlap th leftmost point of the interval
            if (in[1] < newInterval[0]){ 
                result.add(in); 
             // Right most point of the new interval is less than the left most current interval.
             // If this is true, then we add the new interval and update the new inteval to the current interval 
            } else if (newInterval[1] < in[0]){
                result.add(newInterval); 
                newInterval = in; 
            // Here we know that the interval falls within the new interval, so we update the bounds. 
            } else {
                newInterval[0] = Math.min(newInterval[0], in[0]); 
                newInterval[1] = Math.max(newInterval[1], in[1]); 
            }
        }
        result.add(newInterval); 
        
        return result.toArray(new int[result.size()][]); 
    }
}
```
