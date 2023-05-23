# Chess board performance
First, we'll have to figure out how to represent the muscle table as data stored in a variable. On paper, the XO checkerboard is drawn as a pair of horizontal lines and a pair of vertical lines. In this program, the checkerboard will be represented as a list of character strings. Each string of characters represents one of the nine spaces on the chessboard.

Remember that we are placing our chessboard like a numeric keypad on a keyboard. So if a list of 10 string literals is stored in a variable named `board`, then `board[7]` will be the top-left space on the chessboard, `board[8]` will be the top space in the middle and so on. Players will enter a number from 1 to 9 to tell the game which box they want to go in.

# Draw a chess board on the screen
We will define the `drawboard()` function that is responsible for drawing the chessboard as follows:
```
def drawBoard(board):
     print(board[7] + '|' + board[8] + '|' + board[9])
     print('-+-+-')
     print(board[4] + '|' + board[5] + '|' + board[6])
     print('-+-+-')
     print(board[1] + '|' + board[2] + '|' + board[3])
```
The `drawBoard()` function will print the chessboard represented by the `board` parameter. Remember that the chessboard is represented as a list of 10 character strings, where the string at index 1 is the sign on the space 1 on the board. Strings at index 0 will be ignored. The game functions work by passing a list of 10 character strings that are chessboards.

We need to make sure that the spaces are properly aligned in the strings, otherwise the chessboard will look skewed when printed on the screen.

# Allows the player to choose O or X
```
def inputPlayerLetter():
     #Allow users to enter characters
     #Returns the set with the player's character as the first element and the computer's character as the second element.
     letter = ''
     while not (letter == 'X' or letter == 'O'):
         print('Do you want to be X or O?')
         letter = input().upper()

     if letter == 'X':
         return ['X', 'O']
     else:
         return ['O', 'X']
```
# Decide who goes first
```
def whoGoesFirst():
    #Chọn bất kỳ ngẫu nhiên cho phép người chơi đi trước hay không
    if random.randint(0, 1) == 0:
        return 'computer'
    else:
        return 'player'
```
` whoGoesFirst()` function will decide who goes first using the random.randint(0, 1) function.

Next, we will draw characters on the chessboard
```
def makeMove(board, letter, move):
    board[move] = letter
```
Parameters include `board`, `letter` and `move`. The variable `board` is a list of 10 character strings representing the state of the board. The `letter` variable can be the player `letter` variable ('X' or 'O'). The variable `move` is the position on the board the player wants to go.
```
board[move] = letter
```
The above code seems to change one of the elements in the list `board` to the value stored in the variable `letter`. However, since this code is inside a function, the `board` parameter will be omitted when the function returns. So the change to `board` will also be dropped when the function returns?

Absolutely not, because lists have special properties when we pass them as arguments to functions. We are passing a reference to the list, not the list itself. We will learn about the difference between a list and a reference to a list.
# Check if the player wins or not
```
def isWinner(bo, le):
     #Return True if player wins
     #Use bo instead of the full name board and le stands for letter
     return ((bo[7] == le and bo[8] == le and bo[9] == le) or #One top row
     (bo[4] == le and bo[5] == le and bo[6] == le) or #Middle row
     (bo[1] == le and bo[2] == le and bo[3] == le) or #Last row
     (bo[7] == le and bo[4] == le and bo[1] == le) or #Left column
     (bo[8] == le and bo[5] == le and bo[2] == le) or #The middle column
     (bo[9] == le and bo[6] == le and bo[3] == le) or #Right column
     (bo[7] == le and bo[5] == le and bo[3] == le) or #Diagonal
     (bo[9] == le and bo[5] == le and bo[1] == le)) #Diagonal
```
Tên `bo` và `le` là các từ viết tắt cho các tham số của `board` và `letter`. Hãy nhớ rằng, Python không quan tâm đến việc bạn đặt tên cho các biến của mình là gì.

Có tám cách có thể để giành chiến thắng tại Tic Tac-Toe: bạn có thể có một hàng ngang ở các hàng trên cùng, giữa hoặc dưới cùng hoặc các hàng chéo.

Mỗi dòng của điều kiện sẽ kiểm tra xem ba ô cho một dòng nhất định có bằng với ký tự được cung cấp hay không (kết hợp với toán tử `and`). Ta thực hiện kết hợp mỗi dòng bằng cách sử dụng toán tử `or` để kiểm tra tám cách khác nhau. Điều này có nghĩa là chỉ có một trong tám cách sẽ có giá trị là True để chúng ta có thể nói rằng người chơi sở hữu `letter` trong `le` là người chiến thắng.

# Copy Board's data
The `getBoardCopy()` function allows to make a copy of a list containing 10 specified strings representing the checkerboard.
```
def getBoardCopy(board):
    boardCopy = []
    for i in board:
        boardCopy.append(i)
    return boardCopy
```
As the AI algorithm prepares to make a move, it will sometimes need to make modifications to the temporary copy of the chessboard without altering the board. In such cases, we will call this function to make a copy of the list of `board`.

The list stored in `boardCopy` is just an empty list. The `for` loop will iterate over the `board` parameter, adding a copy of the string values to the copy. After the `getBoardCopy()` function creates a copy of the actual chessboard, it returns a reference to this new board in `boardCopy`.
# Check if the square on the chessboard is still available
Cho một bàn cờ caro và một nước đi có thể có, hàm `isSpaceFree()` sẽ trả về liệu nước đi đó có thể thực thi được hay không:
```
def isSpaceFree(board, move):
    #Trả về True nếu nước đi vẫn còn trên bàn cờ
    return board[move] == ' '
```

# Allows the player to enter a move
The `getPlayerMove()` function will ask the player to enter the number for the cell they want to move:
```
def getPlayerMove(board):
     move = ' '
     while move not in '1 2 3 4 5 6 7 8 9'.split() or not isSpaceFree(board, int(move)):
         print('What is your next move? (1-9)')
         move = input()
     return int(move)
```
The loop will ensure that execution will not continue until the player enters an integer between 1 and 9. It also ensures that the entered cell will not be used before, since the checkerboard is passed to function for the board parameter. The two lines of code inside the `while` loop ask the player to enter a number between 1 and 9.

The expression on the left checks if the player's move is equal to '1', '2', '3',..'9' by creating a list with these strings (with the  method  `split()`) and check if the move is in this list. In this expression, '1 2 3 4 5 6 7 8 9'.split() would be [' 1', '2', '3', '4', '5', '6', '7' , '8', '9'].

The expression on the right checks if the move entered by the player is a tile on the chessboard by calling `isSpaceFree()`. Note that the `isSpaceFree()` function returns `True` if the move is already on the chessboard.
# Choose a move from the set of steps
```
def chooseRandomMoveFromList(board, movesList):
     #Returns a valid move from the passed set
     #Returns None if there are no valid moves
     possibleMoves = []
     for i in movesList:
         if isSpaceFree(board, i):
             possibleMoves.append(i)

     if len(possibleMoves) != 0:
         return random.choice(possibleMoves)
     else:
         return None
```
The `board` parameter is a list of character strings representing the checkerboard. The second parameter, `movesList`, is a list of integers of possible cells to select from. For example, if `movesList is [1, 3, 7, 9]`, it means that `selectRandomMoveFromList()` will return the integer that is one of the cells in the corners.

However, `selectRandomMoveFromList()` will initially check if the cell is valid to continue. The `possibleMoves` list is initially an empty list. The `for` loop then iterates through the `movesList`. The moves that will cause the `isSpaceFree()` function to return `True` are added to `possibleMoves` by the `append()` function.

The `possibleMoves` list contains all the moves already in the `movesList` and are the cells that can perform the moves in that place. The program will then check if the list is empty:
```
    if len(possibleMoves) != 0:
        return random.choice(possibleMoves)
    else:
        return None
```
If the list is not empty, there is at least one possible move on the chessboard.

This list may be empty. For example, if `movesList is [1, 3, 7, 9]` but the chessboard is represented by the parameter `board` with all corner tiles occupied, the list of `possibleMoves` will be []. In that case, `len(possibleMoves)` returns 0 and the function returns `None`.
# Build tactics with Game AI
The AI needs to be able to look at the chessboard and decide what kind of empty space it should move. For clarity, we'll label the three types of spaces on the checkerboard: corner, edge, and center.

The AI's Tic-Tac-Toe strategy will follow a simple algorithm, which is a finite sequence of statements to calculate the outcome. A program can use several different algorithms. An algorithm can be represented by a graph. AI's algorithm will calculate the best move to make.

The AI algorithm consists of the following steps:

1..See if the computer can take any action to win the game. If so, the migration will be performed. If not, go to step 2 
2.See if the player can take any action that causes the computer to lose. If yes, move there to block the player. If not, go to step 3 
3.Check if there are any gaps in the corner (gaps 1, 3, 7 or 9). If yes, perform the migration there. If there is no gap in the corner, proceed to step 4 
4.Check if the space in the middle is empty or not. If yes, move there. If not, perform step 5 
5.Move over any space on the sides (2, 4, 6 or 8 gaps). No more steps because side gaps are all that's left if execution reaches step 5


# Generate AI code for computers
```
def getComputerMove(board, computerLetter):
    if computerLetter == 'X':
        playerLetter = 'O'
    else:
        playerLetter = 'X'
```
The first argument is board, which represents the chessboard. The second argument is the character the computer uses, which is 'X' or 'O' in the computerLetter parameter.

The checkerboard AI algorithm works as follows:

1.See if the computer can take any action to win the game. If so, take that action. If not, go to step 2 
2.See if the player can take any action that causes the computer to lose the game. If it is, the computer will move there to block the player. If not, go to step 3 
3.Check if any of the angles (cells 1, 3, 7 or 9) can be taken. If there are no cells, go to step 4
4. Check if the cell in the center is empty or not. If yes, perform the migration there. If not, go to step 5. 
5.Move on any edge (cell 2, 4, 6 or 8). There are no further steps, because the spaces next to it are the only cells left.
The function will return an integer value from 1 to 9 representing the computer's steps.

We will go through how to do the above steps.

# Check if the computer can win in one move
```
    for i in range(1, 10):
        boardCopy = getBoardCopy(board)
        if isSpaceFree(boardCopy, i):
            makeMove(boardCopy, computerLetter, i)
            if isWinner(boardCopy, computerLetter):
                return i
```
The for loop starts first going through each possible step 1 through 9. The code inside the loop simulates what would happen if the computer made that move.

The first line in the loop will make a copy of the board list. This is a simulated move inside the loop and does not change the checkerboard stored in the board variable. The getBoardCopy() function returns an identical but distinct checkerboard list value.

The first if condition checks if the cell has an empty child and if it does, it simulates a move on the copy. If this move is the winning move by the computer, the function returns the integer value of that move.

Otherwise, the loop will end and program execution will continue.


# Check if a player wins on a certain move
```
    for i in range(1, 10):
        boardCopy = getBoardCopy(board)
        if isSpaceFree(boardCopy, i):
            makeMove(boardCopy, playerLetter, i)
            if isWinner(boardCopy, playerLetter):
                return i
```
If the isWinner() function indicates that the player will win on a certain move, the computer will return the move itself to prevent this from happening.

If the player cannot win that move, the for loop ends.


# Check the boxes in the corners, the center and the sides are empty
If the computer cannot make a winning move and does not need to block the player's move, it will move to a corner, center or sides, depending on the space.

The computer will first try to move to one of the gaps in the corner:
```
    move = chooseRandomMoveFromList(board, [1, 3, 7, 9])
    if move != None:
        return move
```
The selectRandomMoveFromList() function call with the list [1, 3, 7, 9] will ensure that the function returns an integer value for one of the spaces in the corners: 1, 3, 7, or 9.

If all corner spaces are used, selectRandomMoveFromList() returns None
```
    if isSpaceFree(board, 5):
        return 5
```
If there is no space left in the corners, it will take the move in tile 5 if it is empty.
```
return chooseRandomMoveFromList(board, [2, 4, 6, 8])
```
This code makes the call to selectRandomMoveFromList(), except that we pass it a list of spaces in adjacent cells: [2, 4, 6, 8]. This function will not return None because adjacent spaces are the only spaces that can be left.



# Check if the chessboard is full or not
```
def isBoardFull(board):
     # Returns True if there are no moves on the board, False otherwise
     for i in range(1, 10):
         if isSpaceFree(board, i):
             return False
     return True
```
This function returns True if the list of 10 character strings in the board argument to which it is passed has an 'X' or 'O' in each index (except index 0 is omitted). The for loop allows us to check indices from 1 to 9 on the list of boards. As soon as it finds an empty space on the chessboard (i.e. when isSpaceFree(board, i) returns True), the isBoardFull() function returns False.

If the loop ends, meaning that the chessboard has no empty cells, the function will return True.



# Loop for the game
The `inputPlayerLetter()` function allows the player to enter X or O values:
```
    playerLetter, computerLetter = inputPlayerLetter()
```
The function returns a list of two strings, ['X', 'O'] or ['O', 'X']. We will use multi-variable assignment to assign values to variables at the same time.

The `whoGoesFirst()` function randomly decides who goes first, returning the string 'player' or 'computer':
```
    turn = whoGoesFirst()
    print('The ' + turn + ' will go first.')
    gameIsPlaying = True
```
The gameIsPlaying variable keeps track of whether the game is still being played or someone has won or drawn.
 


## Take the player's turn
```
    while gameIsPlaying:
        if turn == 'player':
            drawBoard(theBoard)
            move = getPlayerMove(theBoard)
            makeMove(theBoard, playerLetter, move)
```
The turn variable is initially set to "player" or "computer" by the whoGoesFirst() function. The theBoard variable is passed to the drawBoard() function to print the checkerboard on the screen. The getPlayerMove() function then allows the player to enter their move. The makeMove() function adds the player's X or O to the theBoard variable.

After the player enters the move, the program checks if the player won or not:
```
            if isWinner(theBoard, playerLetter):
                drawBoard(theBoard)
                print('Hooray! You have won the game!')
                gameIsPlaying = False
```
If a player doesn't win with their last move, it's possible that their move has filled the entire board. The program will check that condition followed by an else conditional:
```
            else:
                if isBoardFull(theBoard):
                    drawBoard(theBoard)
                    print('The game is a tie!')
                    break
                else:
                    turn = 'computer'
```
## Perform the machine's turn
```
        else:
            move = getComputerMove(theBoard, computerLetter)
            makeMove(theBoard, computerLetter, move)

            if isWinner(theBoard, computerLetter):
                drawBoard(theBoard)
                print('The computer has beaten you! You lose.')
                gameIsPlaying = False
            else:
                if isBoardFull(theBoard):
                    drawBoard(theBoard)
                    print('The game is a tie!')
                    break
                else:
                    turn = 'player'
```
The computer's turn execution code is almost identical to the player's code. And the last piece of code is used to ask the user if they want to play again.
```
    print('Do you want to play again? (yes or no)')
    if not input().lower().startswith('y'):
        break
```
