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
Hàm `getPlayerMove()` sẽ yêu cầu người chơi nhập số cho ô mà họ muốn di chuyển:
def getPlayerMove(board):
    move = ' '
    while move not in '1 2 3 4 5 6 7 8 9'.split() or not isSpaceFree(board, int(move)):
        print('What is your next move? (1-9)')
        move = input()
    return int(move)
