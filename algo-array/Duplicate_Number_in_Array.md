### [Leetcode-287] Find the Duplicate Number.

Given an array nums containing n+1 integers where each integer is between 1 and n(inclusive).

Prove that at least one duplicate number must exist. Assume that there is only one duplicate number, find the one.

Note:
1. You must not modify the array.
2. You must use only O(1) extra space.
3. Runtime complexity should be less than O(n^2).
4. There is only one duplicate number in the array, but it could be repeated more than once.

> **解析**
>
> **pigonhole principle** 或者 **抽屉原理** + **二分查找**。
>
> **pigonhole**：
>
> 这道题题目限定特殊。元素取值范围[1, n]，一共n+1个数。index为0 - (n-1)。

> 例子： [4, 4, 2, 5, 3, 6, 1]
>
> 下标： [0, 1, 2, 3, 4, 5, 6]
>
> 二分查找取mid，当某个小于等于mid的元素重复时，遍历数组，小于等于mid的元素个数应该大于mid值（下标），说明重复元素在小于等于mid的一侧。当小于等于mid的数组元素个数<=mid，说明mid左边部分没有重复元素，重复元素在大于mid的一侧。


```
public class Solution {
    public int findDuplicate(int[] nums) {
        // nums are limited as always valid.
        // So We do not need to judge nums whether exists or not.
        int left = 0;
        int right = nums.length - 1;
        while (left < right) {
            int mid = (left + right) >> 1;
            int count = 0;
            for (int i = 0; i < nums.length; i++) {
                if (nums[i] < mid) {
                    count++;
                }
            }
            if (count <= mid) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        return left;
    }
}
```

-----------
#### 拓展
> 如果数组元素没有限定在[1, n]，而是n个随机元素。
> [100, 102, 99, 150, 102]，要找出数组中重复元素“102”，则上述抽屉原理不能继续使用。

解决方案：
> 1. 使用**set**，遍历一遍，检查set中是否包含该元素，是则为重复元素，否则将元素添加进set。
> 2. 构建**Binary Search Tree**，遍历数组，如果二叉搜索树中包含该元素，则为重复元素，否则将该元素添加进二叉搜索树。

-----
### [Leetcode-] Find all the duplicate in array.

> nums elements: [1, n]

**解法**：

使用**元素标记法**。遍历每个数组元素，将其取绝对值再减1（元素取值[1, n]，减1刚好为下标索引区间[0, n-1]。），将其当做数组索引，并取该索引值下的数组元素为负值。当有重复元素时，则在之前会被标记为负值，存入该元素。

使用set。

弊端是会修改数组元素。
```
public class Solution {
    public List<Inrteger> findAllAuplicates(int[] nums) {
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < nus.length; i++) {
            int index = Math.abs(nums[i]) - 1;
            if (nums[index] < 0) {
                res.add(index + 1);
            } else {
                nums[index] = -nums[index];
            }
        }
        return res;
    }
}
```
