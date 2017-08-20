### [Leetcode-112] Path Sum
Given a binary tree and a sum, determine if the tree has a path-to-leaf path such that adding up all the values along the path equals to the given sum.

>For example: given the binary tree and sum = 22,
>            5
>       4       8
>    11       13    4
>  7    2              1
>return true, as there exist a root-to-left path 5->4->11->2, which sum is 22.

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