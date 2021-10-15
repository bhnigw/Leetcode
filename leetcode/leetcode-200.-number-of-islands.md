---
description: DFS
---

# \[Leetcode]200. Number of Islands

原题地址：[https://leetcode.com/problems/number-of-islands/](https://leetcode.com/problems/number-of-islands/) 关键词：DFS

题意：数小岛数量；\
二维char数组`grid[][]`由0和1组成，0代表水，1代表陆地，陆地连起来组成岛屿，计算岛屿的数量；

例：\
`Input: grid = [ ['1','1','0','0','0'], `\
`                 ['1','1','0','0','0'],  `\
`                 ['0','0','1','0','0'],  `\
`                 ['0','0','0','1','1'] ]  `\
`Output: 3`



算法：DFS

1. 初始化res = 0
2. 遍历grid，遇到island就加一，也就是遇到`'1'`就res++；
3. 然后围绕这个1进行DFS，把与它相临上下左右的`'1'`变为`'0'`，这样可以避免重复扫；
4. 返回res即可；

```
class Solution {
    public int numIslands(char[][] grid) {
        int res = 0;
        
        if (grid == null || grid.length == 0) return 0;
        
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] == '1') { //遇到island就加一
                    res++;
                    dfs(grid, i, j);                               
                } 
            } 
        }
        
        return res;
    }
    
    private void dfs(char[][] grid, int m, int n) {
        if(m < 0 || n < 0 || m >= grid.length || n >= grid[0].length || grid[m][n] == '0') {
            return;
        }//这里if包含了；两个判断，一个是如果grid[m][n]=='0'就直接return
         //第二个判断是：下面的m,n加一减一不能out of bound
        
        grid[m][n] = '0';
        dfs(grid, m - 1, n); //注意这里m-1不能小于0
        dfs(grid, m + 1, n); //这里m+1不能大于等于grid.length
        dfs(grid, m, n + 1);
        dfs(grid, m, n - 1); //这里n+1不能大于等于grid[0].length
    }
}                
```

Time：`O(M×N)`；M、N分别是长和宽；\
解释：取极限，假如所有格子全是1，那么只会进行一次dfs，把M×N个格子涂成0，耗时M×N；遍历剩下的全是0的格子，耗时M×N；总共是2×M×N，所以最后是`O(M×N)`；

Space：`O(M×N)`；M、N分别是长和宽；\
解释：取极限，假如所有格子全是1，那么只会进行一次dfs，此次dfs所有格子涂成0，所耗空间`O(M×N)`

