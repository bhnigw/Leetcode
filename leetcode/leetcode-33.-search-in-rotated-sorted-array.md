---
description: Binary Search
---

# \[Leetcode\]33. Search in Rotated Sorted Array

原题地址：[https://leetcode.com/problems/search-in-rotated-sorted-array/](https://leetcode.com/problems/search-in-rotated-sorted-array/) 关键词：Binary Search

题意：Rotated Sorted Array中寻找目标值。  
一个sorted数组`nums[]`，没有duplicates。数组前面某一段被截取放到了数组末尾，形成了新的数组。给一个整数`target`，求它在数组中的位置index，如果不存在则返回-1。

例1：  
Input: `nums = [4,5,6,7,0,1,2]`, `target = 1`   
Output: 5  
例2：  
Input: `nums = [1]`, `target = 0`  
Output: -1



### 算法：Binary Search





```text
class Solution {
    public int search(int[] nums, int target) {
        if (nums == null || nums.length == 0) return -1;
        
        int peakIndex = findPeakElement(nums);
        
        if (target >= nums[0]) {
            return binarySearch(0, peakIndex, nums, target);
        } else {
            return binarySearch(peakIndex + 1, nums.length - 1, nums, target);
        }
    }
    
    private int findPeakElement(int[] nums) {
        if (nums.length == 1) return 0;
        if (nums[0] < nums[nums.length - 1]) return nums.length - 1;
        
        int index = 0;
        
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] < nums[i - 1]) {
                index = i - 1;
                break;
            }
        }
        
        return index;
    }
    
    private int binarySearch(int left, int right, int[] nums, int target) {
        while (left < right) {
            int mid = left + (right - left) / 2;
            
            if (target > nums[mid]) {
                left = mid + 1;
            } else {
                right = mid;
            }
        }
        
        return nums[right] == target ? right : -1;
    }
}
```









