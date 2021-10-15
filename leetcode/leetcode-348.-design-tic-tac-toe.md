# \[Leetcode]348. Design Tic-Tac-Toe

原题地址：[https://leetcode.com/problems/design-tic-tac-toe/](https://leetcode.com/problems/design-tic-tac-toe/) 

题意：设计一个Tic-Tac-Toe的输赢判定算法。\
输赢条件：在一个`n * n`的正方形格子中，如果同一个玩家在同一行、同一列、或同一对角线上，都放置了自己的棋子，那么他便获得胜利。\
题目给出两个主方法：\
●`TicTacToe(int n)`： 初始化这个`board[][]`的宽度 \
●`int move(int row, int col, int player)`： 整数`player`是玩家的id，整数对`(row, col)`是落点的位置。题目保证所有input都是valid。

例：\
Input：`["TicTacToe", "move", "move", "move", "move", "move", "move", "move"]` \
             `[[3], [0, 0, 1], [0, 2, 2], [2, 2, 1], [1, 1, 2], [2, 0, 1], [1, 0, 2], [2, 1, 1]]` \
Output：`[null, 0, 0, 0, 0, 0, 0, 1]`

Explanation：board的宽度是3，分别有player 1和player 2，最终玩家1胜利，返回胜利玩家的id。



#### 方法1：brute force `O(n ^ 2)`

每走一步，检查整个board，检查所有的行列和对角线，时间`O(n ^ 2)`。



### 方法2：优化后的brute force `O(n)`（推荐）

**核心思想：**只需检查该落点所在的特定行列，如果该行列已被该player填满，则该player胜利。

●如果落点不在对角线上，则只检查该行和该列：

![](../.gitbook/assets/IMG\_6477.jpg)



●如果落点在对角线上，有两种情况：

1. 落在Diagonal上：`row == col`
2. 落在Anti-Diagonal上：**`row == length - 1 - col`**

⚠️  注意：怎样遍历Anti-Diagonal❓

我们把Anti-Diagonal上的格子的index坐标写出来，从上到下依次是：\
`(0, 2)`\
`(1, 1)`\
`(2, 0)`\
总结规律可以发现，横坐标row依次递增，纵坐标col依次递减，横纵坐标row和col加起来刚好等于2，也就是`row + col == length - 1`，变换一下就是`row == length - 1 - col`。所以，在遍历时，只要发现`row == length - 1 - col`，说明该落点就处在Anti-Diagonal上。

![](../.gitbook/assets/IMG\_6478.jpg)

完整代码：

```
class TicTacToe {

    int[][] board;
    int length;
    
    /** Initialize your data structure here. */
    public TicTacToe(int n) {
        board = new int[n][n];
        length = n;
    }
    
    
    public int move(int row, int col, int player) {
        board[row][col] = player; // 把该落点赋值为玩家的id
        
        if (checkRow(row, player) || checkCol(col, player)  //检查行列
           || (row == col && checkDiagonal(player))        //检查对角线
           || (row == length - 1 - col && checkAntiDiagonal(player))) {//检查反对角线
            return player;                   // 任意一个被该player填满，则该player胜利
        }
        
        return 0;
    }
    
    
    private boolean checkRow(int row, int player) {
        for (int i = 0; i < length; i++) {
            if (board[row][i] != player) return false;  // 只检查这一行
        }
        return true;
    }
    
    private boolean checkCol(int col, int player) {
        for (int i = 0; i < length; i++) {
            if (board[i][col] != player) return false; // 只检查这一列
        }
        return true;
    }
    
    private boolean checkDiagonal(int player) {
        for (int i = 0; i < length; i++) {
            if (board[i][i] != player) return false; // 只检查Diagonal
         }
        return true;
    }
    
    private boolean checkAntiDiagonal(int player) {
        for (int i = 0; i < length; i++) {
            if (board[i][length - 1 - i] != player) return false; //只检查AntiDiagonal
        }
        return true;
    }
}
```

Time: `O(n)`; 检查了行列和两个对角线，所以每一步的时间是O(4 \* n)，最终就是O(n)；\
Space: `O(n ^ 2)`; 使用了二维数组记录，也就是`board[][]`的size；



### 方法3：数学技巧 `O(1)`

**核心思想：**只需focus on每一行和每一列。如果在任何时候，某一行列上某玩家的id总数等于了length，则该玩家获胜。 为了记录玩家，设Player1为整数`1`，设Player2为`-1`。初始化两个整数变量，来对Diagonal和Anti-Diagonal计数。每次玩家放置一个棋子时，我们只需要检查该行、列、对角线、反对角线的计数。

```
public class TicTacToe {
    int[] rows;
    int[] cols;
    int diagonal;
    int antiDiagonal;

    public TicTacToe(int n) {
        rows = new int[n];
        cols = new int[n];
    }

    public int move(int row, int col, int player) {
        int currentPlayer = (player == 1) ? 1 : -1;
        
        rows[row] += currentPlayer; // 记录行列
        cols[col] += currentPlayer;
        
        if (row == col) {
            diagonal += currentPlayer; // 记录对角线
        }
        
        if (col == (cols.length - row - 1)) {
            antiDiagonal += currentPlayer;  // 记录反对角线
        }
        
        int n = rows.length;
        
        if (Math.abs(rows[row]) == n ||       // 任意行列上某玩家的id总数等于了length
                Math.abs(cols[col]) == n ||   // 则该玩家获胜
                Math.abs(diagonal) == n ||
                Math.abs(antiDiagonal) == n) {
            return player;
        }
     
        return 0;
    }
}

```

Time: `O(1)`；每走一步，只改变了一个数字；\
Space: `O(n)`；n是数组`rows[]`和`cols[]`的size；



### 本题需要记住的重点：

1. 方法2中，`checkRow(row, player)`方法不需要把board包含在input里，因为board已经是global variable；
2. `checkDiagonal(player)`方法里input只需包含玩家的id





