# Web + Pwn

Web cho mình 1 file binary ELF (file excutable của linux). Bắt tay vào RE file xem sao đã 

![img 1](https://github.com/Cl0wnK1n9/hacker101/blob/main/Capture.JPG)

Hàm main có khai báo biến local_28 là một mảng ký tự gồm 32 phần tử và sau đó dùng memset để tạo vùng nhớ cho biến này và đương nhiên độ dài cùng là 32 bytes tương đương với 32 ký tự. Sau đó tiến hành kiểm tra nếu mảng này không có giá trị nào thì sẽ in ra 2 chuỗi tương ứng. Ngoài ra trong file binary còn có 1 hàm là hàm `printf_flags` nhìn có thể phỏng đoán ta phải gọi đến hàm này để lấy flag.

![img 2](https://github.com/Cl0wnK1n9/hacker101/blob/main/Capture2.JPG)

Và do mình lười nên mình không viết sâu hơn về cái hàm `read_all_stdin` coi như cho mọi người tò mò đi =)). Bài này mindset sẽ là BOF ghi đè lên địa chỉ trả về và địa chỉ trả về đó sẽ là địa chỉ của hàm `printf_flags`. Nếu ai đã quen với BOF thì chắc không cần nói nhiều cơ mà ai chưa biết cách tính buff thì đây nó là như này 

![img 3](https://github.com/Cl0wnK1n9/hacker101/blob/main/Capture3.JPG)

để tính buffer thì chỉ cần quan tâm đến 3 dòng đầu tiên thôi. Đi từ dưới lên ta có `SUB RSP, 0x20` giảm địa chỉ stack đi 0x20 tức 32 bytes để cho `local_28` nhé. Tiếp theo là `PUSH RBP` cộng thêm 8 bytes nữa vậy là ta có 40 bytes trước khi chạm đến return address
Mã khai thác mình để ở file exploit.py
Xin hết ạ !
