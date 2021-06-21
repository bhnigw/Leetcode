---
description: 'Array, Two pointer'
---

# \[Leetcode\]287. Find the Duplicate Number

原题地址：[https://leetcode.com/problems/find-the-duplicate-number/](https://leetcode.com/problems/find-the-duplicate-number/) 关键词：Array, Two pointer

题意：给定一个包含n + 1个整数的数组nums，其数字都在1到n之间（包括1和n），已知nums里有一个重复的数 ，找出这个**重复的数**。（注意这个数可能会重复多次）

方法一：Brute force，两层for loop。Time complexity: O\(n^2\)；Space complexity: O\(1\)

方法二：Sorting，Time complexity: O\(nlogn\)；Space complexity: O\(1\)

```text
class Solution {
    public int findDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i-1]) {
                return nums[i];
            }
        }

        return -1;
    }
}
```



方法三：HashSet，Time complexity: O\(n\)；Space complexity: O\(n\)

```text
class Solution {
    public int findDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<Integer>();
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            }
            seen.add(num);
        }

        return -1;
    }
}
```



方法四\(**重要**\)：**Two pointer**。

对于一个长度为n，包含n个整数，数字都在1到n之间，且无duplicate的乱序数组nums，它具有一个特点，就是如果用当前的nums\[i\]指向nums\[nums\[i\]\]，那最后所有的数都会被指到。

根据这一特性，根据题目的描述，对于一个包含n + 1个整数且数字都在1到n之间的数组nums，一定至少有一个数字a出现了一次重复，那么重复的这个位置，一定会有两个数字同时指向a，这样就形成了一个带环的图，而环的入口/起始点，就是那个重复的数字。

所以这道题就**演变成了一个找环的题**，算法和题目142. Linked List Cycle几乎一样。

定义一个slow pointer，一个fast pointer，slow每次移动到nums\[i\]，fast每次移动到nums\[nums\[i\]\]。那么如果有cycle的话，slow和fast一定会在circle里某处相遇，且相遇时fast pointer所走过的路程一定是slow pointer的两倍。此时把slow放回起点nums\[0\]，然后和fast再同时向前走\(此时fast一次移动一步\)，再次相遇时就是cycle开始的地方，返回这个数即可。

![](.gitbook/assets/img_6044%20%281%29.jpg)

![](.gitbook/assets/img_6045-2%20%281%29.jpg)

```text
class Solution {
    public int findDuplicate(int[] nums) {
        //1.build图
        int slow = nums[0];
        int fast = nums[nums[0]];
        
        while (slow != fast) { //相等了即相遇
            slow = nums[slow];
            fast = nums[nums[fast]];
        }
        
        //2.找circle的起始点
        slow = 0;
        while (slow != fast) {
            slow = nums[slow];
            fast = nums[fast];
        }
        
        return fast;
    }
}
```

Time complexity: O\(n\)；  
**Space complexity: O\(1\)；** 此方法空间复杂度最优

方法五：数学技巧，高斯求和，Gauss Sum；题干是该数字可能会重复多次，所以该方法不适合，但是如果该重复数字之重复了一次，那就可以使用。用数组之和减去1到n的和，就是那个重复的数字。Time: O\(n\)；Space: O\(1\)

```text
class Solution {
    public int findDuplicate(int[] nums) {
        
        //高斯求和
        int n = nums.length - 1;
        int GaussSum = (1 + n) * n / 2;
        
        //数组求和
        int ArraySum = 0;
        for (int num : nums) {
            ArraySum += num;
        }
        
        return ArraySum - GaussSum;
    }
}
```



