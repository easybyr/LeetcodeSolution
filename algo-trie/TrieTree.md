### [Leetcode-421] Maximum XOR of Two Number in an Array?
Given a non-empty array of numbers, a0, a1, a2, ..., an-1, where 0 <= ai <= 2^31.

Find the maximum result of **ai XOR aj**, where 0 <=i, j < n.
Do it in O(n) runtime.
> Input: [3, 10, 5, 25, 2, 8]
>
> Output: 28
>
> Explanation: The maximum result is 5 ^ 25 = 28.

> 一个数组中取 两个数异或 的最大值。

**解析**
> 遍历数组，对每个数的二进制构建一棵字典树。
>
> 再次遍历数组，对每个数的每个二进制位与1异或：数组元素的二进制位为0，则寻找到值为1的子树，数组元素的二进制位为1，则寻找到值为0的子树。(当然也可以与0异或)
>
> 与1异或后子树不为空，则可计数并累加；与1异或后子树为空，则继续向下查找。
>
> **划重点！！！**
> 1. 对数组元素的二进制构建**Trie树**。
> 2. 寻找子树的时候，**与1(或0)异或**。

```
public class Solution {
    public int findMaximumXOR(int[] nums) {
        if (nums == null || nums.length == 0) {
            return 0;
        }
        TrieNode root = new TrieNode();
        // To build Trie Tree.
        for (int num : nums) {
            TrieNode node = root;
            for (int i = 31; i >= 0; i--) {
                int curbit = (num >>> i) & 1;
                if (node.children[curbit] == null) {
                    node.children[curbit] = new TrieNode();
                }
                node = node.children[curbit];
            }
        }

        int max = Integer.MIN_VALUE;

        // To find maximum XOR value.
        for (int num : nums) {
            TrieNode node = root;  // All num start from root node to find。
            int curMax = 0;
            for (int i = 31; i >= 0; i--) {
                int curbit = (num >>> i) & 1;
                if (node.children[curbit ^ 1] != null) {
                    curMax += (1 << i);
                    node = node.children[curbit ^ 1];
                } else {
                    node = node.children[curbit];
                }
            }
            max = curMax > max ? curMax : max;
        }
        return max;
    }

    /**
     * 构建 TrieNode。
     */
    class TrieNode {
        TrieNode[] children;

        public TrieNode() {
            children = new TrieNode();
        }
    }
}
```
