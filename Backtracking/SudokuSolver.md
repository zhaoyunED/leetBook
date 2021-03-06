#SudokuSolver
Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character '.'.

You may assume that there will be only one unique solution.


---




```
思路：
本体是要求解决数独问题。数独盘面是个九宫，每一宫又分为九个小格。

对于每一个空的格子，我们可以放 1-9的任意一个数，放完了之后需要判定放的数是否合适，判断需要考虑3部分：
  当前行
  当前列
  当前小九宫格
这三块都不能出现和该数字相同的数

代码依然来自 leetcode上面的大神

void solveSudoku(vector<vector<char> > &board) {
        solve(board, 0);
}
    
    
bool solve(vector<vector<char> > &board, int position)
{
        if(position == 81)
            return true;

        int row = position / 9;
        int col = position % 9;
        if(board[row][col] == '.')
        {
            for(int i = 1; i <= 9; i ++)
            {//try each digit
                board[row][col] = i + '0';
                if(check(board, position))
                    if(solve(board, position + 1))
                    //only return valid filling
                        return true;
                board[row][col] = '.';
            }
        }
        else
        {
            if(solve(board, position + 1))
            //only return valid filling
                return true;
        }
        return false;
}
    
    
bool check(vector<vector<char> > &board, int pos)
{
        int v = pos/9;
        int h = pos%9;
        char target = board[v][h];
        //row
        for(vector<char>::size_type st = 0; st < 9; st ++)
        {
            if(st != h)
            {
                if(target == board[v][st])
                    return false;
            }
        }

        //col
        for(vector<char>::size_type st = 0; st < 9; st ++)
        {
            if(st != v)
            {
                if(target == board[st][h])
                    return false;
            }
        }

        //确定小九宫格 的 起始行 起始列
        int beginx = v/3*3;
        int beginy = h/3*3;
        for(int i = beginx; i < beginx+3; i ++)
        {
            for(int j = beginy; j < beginy+3; j ++)
            {
                if(i != v && j != h)
                {
                    if(target == board[i][j])
                        return false;
                }
            }
        }

        return true;
}
```