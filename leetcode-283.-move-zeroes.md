# \[Leetcode\]283. Move Zeroes

题目链接：[https://leetcode.com/problems/move-zeroes/](https://leetcode.com/problems/move-zeroes/)

题意：一个整数array，把所有的0移到右边，其余数左移且顺序不变  
`Input: nums = [0,1,0,3,12]   
Output: [1,3,12,0,0]`



算法：要做到Space Optimal，就不能另外创建数组，就在原数组上操作；

1. 先设置一个index为0
2. 第一次遍历数组，遇到不是0的，就依次放在数组最左边 `nums[index] = 非零数;`然后index++；
3. 第一次遍历完后，此时index为数组改动后所有非零数的右边一位的index，从这index开始往后就应该全部为0；
4. 第二次遍历数组，从index开始到末尾，全部赋值0即可；

```text
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) return; //null check
        
        int index = 0;
        
        for (int num : nums) { //不为0的挨个排到原数组左边
            if (num != 0) {
                nums[index] = num;
                index++;
            }
        }
        
        while (index < nums.length) { //右边全部赋值0
            nums[index] = 0;
            index++;
        }
    }
}
```

或者：

```text
class Solution {
    public void moveZeroes(int[] nums) {
        if (nums == null || nums.length == 0) return;
        
        int index = 0;
        
        for (int num : nums) {
            if (num != 0) {
                nums[index] = num;
                index++;
            }
        }
        
        for (int i = index; i < nums.length; i++) { //更好理解
            nums[i] = 0;
        }
    }
}
```

Time: O\(n\);  
Space: O\(1\);

