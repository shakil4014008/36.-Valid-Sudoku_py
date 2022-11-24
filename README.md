# 36.-Valid-Sudoku_py

````py
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        N = 9

        # Use hash set to record the status
        rows = [set() for _ in range(N)]
        cols = [set() for _ in range(N)]
        boxes = [set() for _ in range(N)]

        for r in range(N):
            for c in range(N):
                val = board[r][c]
                # Check if the position is filled with number
                if val == ".":
                    continue

                # Check the row
                if val in rows[r]:
                    return False
                rows[r].add(val)

                # Check the column
                if val in cols[c]:
                    return False
                cols[c].add(val)

                # Check the box
                idx = (r // 3) * 3 + c // 3
                if val in boxes[idx]:
                    return False
                boxes[idx].add(val)

        return True
        
        
        
        2nd but similar approach: 
        class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
#         idea is row, col, block check and if every condition pass then valid 

        def map_block(i):
            if i < 3: return 0
            elif i < 6: return 1
            elif i < 9: return 2
            
        block_numbers = [[0, 1, 2],[3, 4, 5], [6, 7, 8]]
        block_sets = [set() for i in range(9)]
        col_sets = [set() for i in range(9)]
        row_sets = [set() for i in range(9)]
        
        for i in range(9):
            for j in range(9):
                if board[i][j] not in '123456789':
                    continue
                if board[i][j] in row_sets[i]:
                    return False
                row_sets[i].add(board[i][j])
                
                if board[i][j] in col_sets[j]:
                    return False
                col_sets[j].add(board[i][j])
                
                x, y = map_block(i), map_block(j)
                block_set = block_sets[block_numbers[x][y]]
                if board[i][j] in block_set:
                    return False
                
                block_set.add(board[i][j])
        
        return True
                
        
````py
