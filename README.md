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
