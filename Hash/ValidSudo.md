#ValidSudo
Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.


A partially filled sudoku which is valid.

Note:
A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.


---




```
思路：
只是简单的检查一下数独板上的数字是否冲突
used1 表示 对应的数字是否在某行出现过
used2 表示 对应的数字是否在某列出现过
used3 表示 对应的数字是否在某小九宫格出现过

bool isValidSudoku(vector<vector<char> > &board) 
{
      int used1[9][9] = {0}, used2[9][9] = {0}, used3[9][9] = {0};

      for(int i = 0; i < board.size(); ++ i)
            for(int j = 0; j < board[i].size(); ++ j)
                if(board[i][j] != '.')
                {
                    int num = board[i][j] - '0' - 1, k = i / 3 * 3 + j / 3;
                    if(used1[i][num] || used2[j][num] || used3[k][num])
                        return false;
                    used1[i][num] = used2[j][num] = used3[k][num] = 1;
                }

      return true;
}
```