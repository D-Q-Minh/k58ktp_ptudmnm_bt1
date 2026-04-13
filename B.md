# B.Cài đặt Ubuntu + Docker
## 1. Cài đặt hệ điều hành Ubuntu 24.04.4 LTS
##### Cài đặt Ubuntu 24.04.4 LTS
<img width="364" height="77" alt="image" src="https://github.com/user-attachments/assets/55ea90ff-b718-45af-bdc0-b78ececcee35" />

##### Cấu hình mạng trong Ubuntu (và công cụ giả lập) để cho phép truy cập SSH vào Ubuntu từ cmd của windows:
###### Truy cập SSH vào Ubuntu từ cmd:
<img width="656" height="515" alt="Cấu hình để SSH từ Windows CMD - Screenshot 2026-04-13 031925" src="https://github.com/user-attachments/assets/0f4842bb-0970-4e90-ac49-c4ed0664a051" />

## 2. các lệnh cơ bản của docker:
###### Liệt kê các file trong thư mục: ls
###### Tạo thư mục: mkdir nameFolder
###### Chuyển thư mục làm việc: cd path
###### Copy file: cp file_nguồn path/file_đích
###### Thay đổi quyền thao tác file: sudo chmod xxx filename
###### Edit file: sudo nano tenfile
###### CTRL+o : lưu nội dung sau khi edit
###### CTRL+x : thoát edit file
###### Xem ip của máy ubuntu: ip -4 addr
###### Bonus: Các lệnh thông dụng khác:
######  chmod: Thay đổi quyền truy cập tệp tin/thư mục.
######  chown: Thay đổi chủ sở hữu của tệp tin/thư mục.
######  cat: Hiển thị nội dung tập tin.
######  grep: Tìm kiếm một mẫu văn bản trong file.
######  find: Tìm kiếm tệp tin hoặc thư mục dựa trên các tiêu chí
######  nano: Trình soạn thảo văn bản trong terminal.
######  rm: Xóa tập tin (rm file.txt).
######  rmdir: Xóa thư mục rỗng.
######  rm -rf: Xóa thư mục và toàn bộ nội dung bên trong (cẩn thận khi sử dụng).
######  pwd: Hiển thị đường dẫn đầy đủ của thư mục hiện tại.

## 3. Cài đặt docker cho Ubuntu
## 4. Phiên bản docker:
<img width="392" height="39" alt="image" src="https://github.com/user-attachments/assets/7b2715d6-a756-4921-b977-0b2d4fd82ad4" />

## 5. Cấu hình để docker chạy mà không cần tiền tố sudo
<img width="439" height="59" alt="Cấu hình để docker chạy mà không cần tiền tố sudo - Screenshot 2026-04-13 032609" src="https://github.com/user-attachments/assets/9845dc66-52ee-4046-9f4f-80d491e75299" />

## 6. Tìm hiểu tập lệnh của docker và docker compose

## 7. Đảm bảo tường lửa trên Ubuntu đã cho phép các cổng 80, 1880, 9630 (Lệnh: sudo ufw allow ...)
