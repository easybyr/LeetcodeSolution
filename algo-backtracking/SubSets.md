### [LeetCode-78] SubSets
> Given a set of distinct integers, nums, return the possible subsets.


#### 回溯 + 递归

**时间复杂度** O(n^2)

**空间复杂度** O(n)

##### 代码

```
public class Solution {
    public List<List<Integer>> subSets(int[] nums) {
        List<Integer> list = new ArrayList<>();
        List<List<Integer>> res = new ArrayList<>();
        helper(nums, res, list, 0);
        return res;
    }

    private void helper(int[] nums, List<List<Integer>> res, List<Integer> list, int pos) {
        res.add(new ArrayList<>(list));
        for (int i = pos; i < nums.length; i++) {
            list.add(nums[i]);
            helper(nums, res, list, i + 1);
            list.remove(list.size() - 1);
        }
    }
}
```

### [LeetCode-90] SbuSets II
> Given a collection of integer that may contain duplicates, nums, return the possible subsets.

#### 回溯 + 递归，首先排序。递归的时候跳过重复元素或者使用Set。

**时间复杂度** O(n^2)

**空间复杂度** O(n)

##### 思路

##### 注意
1. 包含重复元素，注意去重。
2. 首先排序。然后跳过重复元素。
3. 如果没有使用排序去掉重复元素，则可以使用Set<List\<Integer\>>，但是也要首先排序。
4. 注意回溯：list.remove(list.size() - 1);
5. 递归方法helper()需要一个int入参 pos，因为每次递归都是从当前数组元素的下一个元素位置开始。
6. 递归的pos位置为 i + 1。
7. 每次添加结果集，都是另一份拷贝。如：res.add(new ArrayList<Integer>(list))。

##### 代码

```
/**
 * 使用Set去掉重复结果。首先也得排序。
 * 排序原因：Set中元素是List，如果不排序，
 * 即使list中元素都相同，顺序不同也是不同的list。
 */
public class Solution {
    public List<List<Integer>> subSetsWithDup(int[] nums) {
        List<Integer> list = new ArrayList<>();
        Set<List<Integer>> resSet = new HashSet<>();
        Arrays.sort(nums);   // 首先排序
        helper(nums, resSet, list, 0);
        return new ArrayList<List<Integer>>(resSet);
    }

    private void helper(int[] nums, Set<List<Integer>> resSet, List<Integer> list, int pos) {
        resSet.add(new ArrayList<>(list));
        for (int i = 0; i < nums.length; i++) {
            list.add(nums[i]);
            helper(nums, resSet, list, i + 1);
            list.remove(list.size() - 1);
        }
    }
}

```

```
/**
 * 不使用Set，对于重复元素，需要排序后跳过重复元素。
 */
 public class Solution {
     public List<List<Integer>> subSetsWithDup(int[] nums) {
         List<Integer> list = new ArrayList<>();
         List<List<Integer>> res = new ArrayList<>();
         helper(nums, res, list, 0);
         return res;
     }

     private void helper(int[] nums, List<List<Integer>> res, List<Integer> list, int pos) {
         res.add(new ArrayList<>(list));
         int i = pos;
         while (i < nums.length) {
             list.add(nums[i]);
             helper(nums, res, list, i + 1);
             list.remove(list.size() - 1);
             i++;
             // 跳过重复元素, 出现 i-1，避免数组越界。
             while (i < nums.length && nums[i] == nums[i - 1]) {
                 i++;
             }
         }
     }
 }
```
