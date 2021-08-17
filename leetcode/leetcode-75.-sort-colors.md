# \[Leetcode\]75. Sort Colors

原题地址：[https://leetcode.com/problems/sort-colors/](https://leetcode.com/problems/sort-colors/) 关键词：

题意：颜色分类；  
给一个乱序的数组，包含整数0、1、2代表三种颜色，对它们进行排序，使得相同颜色的元素相邻，并按照0、1、2顺序排列。

要求：不能使用sort\(\)方法；只能扫描一趟；不能用额外的空间，**space只能是O\(1\)；**

例：  
Input: `nums = [2,0,2,1,1,0]`  
Output: `[0,0,1,1,2,2]`



### 算法：

思路类似[283. Move Zeroes](https://bhnigw.gitbook.io/leetcode/leetcode/leetcode27.-remove-element-tong-lei-ti-zong-jie/leetcode-283.-move-zeroes)；





```text
class Solution {
    public void sortColors(int[] nums) {
        if (nums == null || nums.length == 0) return;
        
        int zero = -1;
        int two = nums.length;
        
        int index = 0;
        while (index < two) {
            if (nums[index] == 0) {
                zero++;
                swap(nums, zero, index);     
                index++;
            } else if (nums[index] == 1) {
                index++;
            } else {
                two--;
                swap(nums, two, index);
                                       // 注意这里index没有++
            }
            
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }
}
```





### 要注意的重点：

1. 遇到数字2的时候，index不能++





