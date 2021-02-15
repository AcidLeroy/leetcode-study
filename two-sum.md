# Two sum

We can easily solve this problem using the O(N^2) approach with brute force using the following solution: 

## Brute force solution
```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        for (int i = 0; i < nums.length; i++ ){
            for (int j = i+1; j < nums.length; j++){
                if (nums[i] + nums[j] == target){
                    int[] arr = {i, j}; 
                    return arr; 
                }
            }
        }
        int[] arr = {-1, -1}; 
        return arr; 
    }
}
```

## Using a hash map
We can improve the solution by first hashing the array and then checking to see if we can find the sum. This means we are using more
memory but we now onl use O(N) time complexity. 

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        // map value to index.
        HashMap<Integer, Integer> mp = new HashMap<Integer,Integer>(); 
        // Populate the hashmap
        for (int i = 0; i < nums.length; i++){
            mp.put(nums[i], i); 
        }
        for (int i = 0; i < nums.length; i++){
            Integer diff = target - nums[i]; 
            Integer idx = mp.get(diff); 
            if (idx == null) continue; 
            if (idx != i){
                return new int[]{i, idx}; 
            }
        }
        throw new IllegalArgumentException("No two sum solution");
    }
}
```
