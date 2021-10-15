---
description: Backtrack
---

# \[Leetcode]90. Subsets II

原题地址：[https://leetcode.com/problems/subsets-ii/](https://leetcode.com/problems/subsets-ii/) 关键词：Backtrack

题意：给一个含有duplicate的数组，输出所有的子集（包括空集和它本身）；要求输出结果中不含重复子集；

例：\
Input: `nums = [1, 2, 3, 2] `\
Output: `[[],[1],[1,2],[1,2,2],[1,2,2,3],[1,2,3],[1,3],[2],[2,2],[2,2,3],[2,3],[3]]`



#### 详细图解：

![](../../.gitbook/assets/90\_approach3\_1.png)



#### 算法:

使用[backtrack](https://bhnigw.gitbook.io/-1/backtrack-mo-ban)，如何去重复呢？

首先哪里会出现重复呢？答：比如从`[1]`开始加，加了2后变为`[1, 2]`，backtrack后，第一个2后面的元素依然是2，如果`[1]`再加就再一次变成了`[1, 2]`，出现重复；所以，我们要**先把数组sort一下**，然后在backtrack的时候，如果遇到相同的元素，需要skip掉。

#### 代码结构：

1. 无需null check；初始化二维List作为res，初始化一维List作为backtrack时候的current Subset；
2. 给数组排序sort，为后面去重复做准备；
3. 无需for循环遍历数组，直接用0作为初始index进入helper方法；
4. 在helper方法内：
   1. 首先把当前此刻最新的currentSubset加入结果集（第一轮加入的是空集）
   2. 从当前输入的index开始for循环，每一轮的for 循环都有四个操作：
      1. 去重复。第一轮for循环的时候不用比较，因为是从i == index开始的；进入第二轮for循环的时候，i大于了index，所以比较第二轮for循环的`nums[i]`和上一个的`nums[i - 1]`是否相等，相等的话就skip；（对应下面第1步）
      2. 把当前数字`nums[i]`加入curren subset；（对应下面第2步）
      3. 开始递归找此刻i + 1的subset；（对应下面第3步）
      4. ★每一轮for循环结束前，都要去掉curren subset里最后一个元素（因为要backtrack到上一轮给末尾加入新的元素，详细看上图和[backtrack讲解](https://bhnigw.gitbook.io/-1/backtrack-mo-ban)）（对应下面第4步）

```
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> currentSubset = new ArrayList<>();
        Arrays.sort(nums);
        
        helper(nums, 0, currentSubset, res);

        return res;
    }
    
    private void helper(int[] nums, int index, List<Integer> currentSubset, List<List<Integer>> res) {
        res.add(new ArrayList<>(currentSubset)); //注意一定要new ArrayList
        
        for (int i = index; i < nums.length; i++) {
            if(i > index && nums[i] == nums[i - 1]) continue; //第1步

            currentSubset.add(nums[i]);                     //第2步
            helper(nums, i + 1, currentSubset, res);        //第3步
            currentSubset.remove(currentSubset.size() - 1); //第4步
        }
    }
}
```

Time：O(n × 2 ^ n)；\
sort的时间O(nlogn)忽略不计； 

Space：O(n)；\
sort的空间O(logn)忽略不计； 

★复杂度的详细讲解查看[78.Subsets](https://bhnigw.gitbook.io/leetcode/leetcode-78.-subsets)

### 要记住的重点：

1. 主函数起始的时候不用for循环，直接开始backtrack；
2. helper方法里所有的四步操作都在for循环里；
3. 不用任何return；
4. 注意如何skip重复：`if(i > index && nums[i] == nums[i - 1]) continue;`
5. backtrack最后一步一定要去除current subset里最后一个元素；
