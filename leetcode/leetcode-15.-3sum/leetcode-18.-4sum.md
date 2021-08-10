---
description: 'Array, Two pointer'
---

# \[Leetcode\]18. 4Sum

原题地址：[https://leetcode.com/problems/4sum/](https://leetcode.com/problems/4sum/)关键词：Array, Two pointer

题意：给你一个数组`nums`\(可能含有duplicates\)，和一个目标值`target`。找出并返回满足条件的四元组`nums[a] + nums[b] + nums[c] + nums[d] == target`，（a、b、c 和 d 互不相同）可以按任意顺序返回答案 。



### 算法：Two pointer

核心思想与3Sum完全相同，区别是最外面多了一层for循环

```text
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
		List<List<Integer>> res = new ArrayList<>();
		if (nums.length < 4) return res; // corner case
        
		Arrays.sort(nums);

		for (int i = 0; i < nums.length; i++) { // 与3sum的区别
			if (i > 0 && nums[i] == nums[i - 1]) continue; // skip duplicates

      // 从这里开始是3sum
			for (int j = i + 1; j < nums.length - 2; j++) {
				if (j > i + 1 && nums[j] == nums[j - 1]) continue; // skip duplicates
				
        int left = j + 1;
				int right = nums.length - 1;

				while (left < right) {
					int sum = nums[i] + nums[j] + nums[left] + nums[right];
					if (sum < target) {
						left++;
						while (nums[left] == nums[left - 1] && left < right) left++; // skip duplicates
					} else if (sum > target) {
						right--;
						while (nums[right] == nums[right + 1] && left < right) right--; // skip duplicates
					} else {
						res.add(Arrays.asList(nums[i], nums[j], nums[left], nums[right]));
						left++;
						right--;
                        
						while (nums[left] == nums[left - 1] && left < right) left++; // skip duplicates
						while (nums[right] == nums[right + 1] && left < right) right--; // skip duplicates
					}
				}
			}
		}
		
		return res;
	}
}
```

Time：`O(n^3)`；三层循环  
Space：`O(logn)`；sort

