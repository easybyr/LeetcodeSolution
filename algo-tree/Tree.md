#### Unique Binary Search Tree
> Given n, how many structurally unique BST's(binary search tree) that store value 1...n? \
> 给定n, 求唯一二叉树的个数。

> 例如n=3, 一共可以组成5个BST。

##### 解析
n = 0, fn = 1; \
n = 1, fn = f(0) * f(0) = 1; \
n = 2, fn = f(0) * f(1) + f(1) * f(0) = 2; \
n = 3, fn = f(0) * f(2) + f(1) * f(1) + f(2) * f(0)
          = 1 * 2 + 1 * 1 + 2 * 1 = 5;  \
n = n, fn = f(0) * f(n - 1) + f(1) * f(n-2) + f(2) * f(n - 3) + ... + f(n - 2) * f(1) + f(n - 1) * f(0);

> 左子树0个节点的子树个数 * 右子树（n-1）个节点的子树个数 +
> 左子树1个节点 * 右子树（n-2）个节点 + ...+左子树（n-1）个节点 * 右子树0个节点。

###### 拓展
- 这是一道**卡特兰数**的算法题。
- 卡特兰数：H(n) = (2n)! / ((n+1)! * n!)

###### 代码
```
public Solution {
    public int uniqueBST(int n) {
        int[] fn = new int[n + 1];
        fn[0] = 1;
        fn[1] = 1;
        for (int i = 2; i <= n; i++) {
            int count = 0;
            for (int j = 0; j < i; j++) {
                count += fn[j] * fn[i-j-1];
            }
            fn[i] = count;
        }
        return fn[n];
    }

}
```
