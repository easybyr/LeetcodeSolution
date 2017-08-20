### [Leetcode-108] Convert Sorted Array to Binary Search Tree
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

**Note**:
Binary Search Tree: 左子树 < root < 右子树
二分法，中点为root，左边子数组为左子树，右边子数组为右子树。

#### Solution
```
public class Main {
    public TreeNode sortedArrayToBST(int[] nums) {
        if (nums == null) {
            return null;
        }
        return helper(nums, 0, nums.length);
    }

    private TreeNode helper(int[] nums, int low, int high) {
        if (low > high) {
            return null;
        }
        int mid = (low + high) >> 1;
        TreeNode root = new TreeNode(nums[mid]);
        root.left = helper(nums, 0, mid - 1);
        root.right = helper(nums, mid + 1, high);
        return root;
    }
}
```
