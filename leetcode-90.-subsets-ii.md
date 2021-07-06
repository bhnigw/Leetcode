---
description: Backtrack
---

# \[Leetcode\]90. Subsets II

原题地址：[https://leetcode.com/problems/subsets-ii/](https://leetcode.com/problems/subsets-ii/) 关键词：Backtrack

题意：给一个含有duplicate的数组，输出所有的子集（包括空集和它本身）；要求输出结果中不含重复子集；

例：  
Input: `nums = [1,2,2]`   
Output: `[[],[1],[1,2],[1,2,2],[2],[2,2]]`

算法：

![](.gitbook/assets/90_approach3_1.png)

```text
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> currentSubset = new ArrayList<>();
        Arrays.sort(nums);
        
        helper(nums, 0, currentSubset, res);

        return res;
    }
    
    private void helper(int[] nums, int index, List<Integer> currentSubset, List<List<Integer>> res) {
        res.add(new ArrayList<>(currentSubset));   
        
        for (int i = index; i < nums.length; i++) {
            if(i > index && nums[i] == nums[i - 1]) continue;

            currentSubset.add(nums[i]);                     //1
            helper(nums, i + 1, currentSubset, res);        //2
            currentSubset.remove(currentSubset.size() - 1); //3
        }
    }
}
```

Time：O\(n × 2 ^ n\) 

Space：O\(n\)



