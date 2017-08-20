### [Leetcode-112] Path Sum
Given a binary tree and a sum, determine if the tree has a path-to-leaf path such that adding up all the values along the path equals to the given sum.

#### Solution
```
public class Main {
    public boolean hasPathSum(TreeNode root, int sum) {
        if (root == null) {
            return false;
        }
        if (root.val == sum && root.left == null && root.right == null) {
            return true;
        }
        return hasPathSum(root.left, sum - root.val) || hashPathSum(root.right, sum - root.val);
    }
}
```
