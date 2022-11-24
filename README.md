# 36.-Valid-Sudoku_py

````py
 class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
    # T = O(1), S = O(1)
    
        row = [set() for i in range(9)]
        col = [set() for i in range(9)]
        box = [[set() for i in range(3)], \
               [set() for i in range(3)],  \
               [set() for i in range(3)]]

        def determineBox(i):
            if i < 3: return 0
            elif i < 6: return 1
            elif i < 9: return 2

        for i in range(9):
            for j in range(9):

                if board[i][j] not in '123456789': 
                    continue 
                if board[i][j] in row[i]:
                    return False
                row[i].add(board[i][j])

                if board[i][j] in col[j]:
                    return False
                col[j].add(board[i][j])
                
                t = determineBox(i)
                x = determineBox(j)
                if board[i][j] in box[t][x]: 
                    return False
                box[t][x].add(board[i][j])

        return True

        
        
````py
