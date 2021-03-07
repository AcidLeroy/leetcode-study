# Jump game
This is another Dynamic Programming that I failed to grock immediately. For these types of problems, I seem to be able to quickly come up with a backtracking solution, 
but then I struggle to find the optimal solution. For this particular problem, there is a greedy approach which makes solving it much faster. 

##❌ Optimized backtracking
In this solution, I used a recursive approach and then added memoization to the hot spots. However, I still ended up with `Time Limit Exceeded` with this solution

```java
class Solution {
    
    HashMap<Integer, Boolean> memo; 
    
    public boolean jump(int[] nums, int curr){
        // System.out.println("curr = " + curr); 
        int lastIdx = nums.length - 1;
        if (curr == lastIdx) return true;
        
        if (memo.containsKey(curr)) {
            //System.out.println("In map"); 
            return memo.get(curr); 
        }
        
        int maxSteps = nums[curr]; 
        
        for (int i = curr + 1; i <= lastIdx && i <= curr+maxSteps; i++) {
            boolean result = jump(nums, i); 
            if (result) {
                memo.put(curr, true); 
                return true;
            }
        }
        memo.put(curr, false); 
        return false; 
        
    }
    
    public boolean canJump(int[] nums) {
        memo = new HashMap<Integer, Boolean>(); 
        return jump(nums, 0); 
    }
}
```
