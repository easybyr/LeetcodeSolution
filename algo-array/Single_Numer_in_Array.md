## [Leetcode-540] Single Element in a Sorted Array

Given a sorted array consisting of only integers where every element appears twice except for one element which appears only once.

>Example:
>Input: [1, 1, 2, 3, 3, 4, 4, 8, 8]
>Output: 2

>Note: You solution should run in O(logn) time and O(1) space.

##### Solution
```
public class Main {
    // solution with O(n) time complexity;
    public int singleElement(int[] nums) {
        int res = 0;
        for (int i = 0; i < nums.length; i++) {
            res ^= nums[i]; 
        }
        return res;
    }

    // solution with O(logn) time complexity.
    public int singleElement(int[] nums) {

    }
}
```