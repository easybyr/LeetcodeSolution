### [Leetcode-110] Given a bianry tree, determine if it is height-balanced.

**Note**
二叉平衡树：左子树高度与右子树高度小于等于1。

#### Solution
```
public class Main {
    public boolean isBalancedTree(TreeNode root) {
        if (root == null) {
            return true;
        }
        int l = maxHeight(root.left);
        int r = maxHeight(root.right);
        return Math.abs(l - r) <= 1 && isBalancedTree(root.left) && isBalancedTree(root.right);
    }

    private int maxHeight(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int left = maxHeight(root.left);
        int right = maxHeight(root.right);
        return (left > right ? left : right) + 1;
    }
}
```