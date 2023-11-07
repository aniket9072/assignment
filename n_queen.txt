import time

def solveNQueenUtils(board,cols,diag1,diag2,col,n):
    if(col >= n):
        return True 
    
    for row in range(n):
        if(cols[row] == 0 and diag1[row+col] == 0 and diag2[n+col-row-1] == 0):
            board[row][col] = 1 
            cols[row] = diag1[row+col] = diag2[n+col-row-1] = 1
            if(solveNQueenUtils(board,cols,diag1,diag2,col+1,n)):
                return True 
            
            board[row][col] = 0
            cols[row] = diag1[row+col] = diag2[n+col-row-1] = 0
            
    return False

def solveNQueen(n):
    board = [[0 for _ in range(n)] for _ in range(n)]
    cols = [0]*n 
    diag1 = [0]*(2*n-1)
    diag2 = [0]*(2*n-1)
    
    if(solveNQueenUtils(board,cols,diag1,diag2,0,n)):
        for i in range(n):
            for j in range(n):
                print(board[i][j],end=" ")
            print("\n")
        return True 
    return False 


n = int(input("Enter The Value of N : "))
start = time.time()
if not solveNQueen(n):
    print("No Solution Exist")
end = time.time()
print("Time Complexity: ",end-start)