### [Leetcode-101] Symmetric Tree

Given a binary tree, check whether it is a mirror of itself.
For example, this binary tree, [1, 2, 2, 3, 4, 4, 3] is symmetric.
                1
            2       2
         3     4  3    4

##### Solution: DFS

```
public class Main {
    public boolean isSymmetric(TreeNode root) {
        return root == null || isMirror(root.left, root.right);
    }

    private boolean isMirror(TreeNode node1, TreeNode node2) {
        if (node1 == null && node2 == null) {
            return true;
        }
        if (node1 == null && node2 != null || node1 != null && node2 == null || node1.val != node2.val) {
            return false;
        }
        return isMirror(node1.left, node2.right) && isMirror(node1.right, node2.left);
    }
}
```