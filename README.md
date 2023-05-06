#Biểu diễn bảng cờ
Đầu tiên, chúng ta sẽ phải tìm ra cách biểu diễn bảng cơ dưới dạng dữ liệu được lưu trong một biến. Trên giấy, bảng cờ caro XO được vẽ dưới dạng một cặp đường ngang và một cặp đường dọc. Trong chương trình này, bảng cờ caro sẽ được biểu diễn dưới dạng danh sách các chuỗi ký tự. Mỗi chuỗi ký tự đại diện cho một trong chín khoảng trống trên bàn cờ.

Nhớ rằng chúng ta đang đặt bàn cờ của mình giống như một bàn phím số trên bàn phím. Vì vậy, nếu một danh sách có 10 chuỗi ký tự được lưu trữ trong một biến có tên là board, thì board[7] sẽ là khoảng trống trên cùng bên trái trên bàn cờ, board[8] sẽ là khoảng trống bên trên cùng ở giữa và cứ như thế. Người chơi sẽ nhập một số từ 1 đến 9 để cho trò chơi biết họ muốn đi vào ô nào.
#Vẽ bàn cờ lên trên màn hình
Chúng ta sẽ định nghĩa hàm drawboard() có nhiệm vụ thực hiện vẽ bàn cờ như sau:
```
function test() {
  console.log("notice the blank line before this function?");
}
```
Hàm drawBoard() sẽ thực hiện in ra bàn cờ được biểu thị bằng tham số board. Hãy nhớ rằng bàn cờ được biểu diễn dưới dạng danh sách bao gồm 10 chuỗi ký tự, trong đó chuỗi ký tự ở chỉ số 1 là dấu trên khoảng trống 1 trên bàn cờ. Chuỗi ký tự tại chỉ số 0 sẽ bị bỏ qua. Các hàm của trò chơi hoạt động bằng cách truyền một danh sách gồm 10 chuỗi ký tự là bàn cờ.

Ta cần đảm bảo rằng các khoảng trống sẽ được căn đúng trong các chuỗi, nếu không, bàn cờ trông sẽ bị lệch khi in trên màn hình.