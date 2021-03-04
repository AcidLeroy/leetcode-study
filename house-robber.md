# House Robber Problem

I attempted to solve this probme in under 20 minutes and failed because of my approach. I thought an efficient way to solve this problem 
would be to keep track of hosues that "couldn't" be robbed and then go from there. I got stuck because I started thinking about
how to end my recursion (I was attemtpting to recurse through the possibilities). The problem can be solved much easier.

Basically the Robber has two options: 
1. Rob the current (or)
2. Don't rob the current house

When you find this out, you can see that ther are only *two* possibilities when recursing. So the solution would look something like this: 
`rob(i) = Math.max(rob(i-2) + houseValue, /* OR */ rob(nums, i-1))`
The solution for this is below: 

## Naive Solution (no memo)
```java
class Solution {
    
   public int rob(int[] nums) {
    return rob(nums, nums.length - 1);
}
private int rob(int[] nums, int i) {
    if (i < 0) {
        return 0;
    }
    return Math.max(rob(nums, i - 2) + nums[i], rob(nums, i - 1));
}
}
```

## Better solution using memoization
A better solution would be to use memoization. 
