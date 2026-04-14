# C. Cấu hình docker compose:
####
- Tạo thư mục: ~/myapp
- Chuyển vào trong thư mục ~/myapp
- Tạo thư mục: ./myweb
- Tạo file ./myweb/index.html (với nội dung là thông tin cá nhân của em)
#### 
<img width="788" height="650" alt="image" src="https://github.com/user-attachments/assets/86dfdc19-e697-4670-8ee5-59df4b31bac9" />

#### Tạo file docker-compose.yml để nó sẽ có các dịch vụ sau:
- Khai báo sử dụng nodered/node-red, cổng 1880, dữ liệu nằm tại thư mục ./nodered
- Khai báo sử dụng nginx, cổng 80, cấu hình trong file ./nginx/nginx.conf
- Mount thư mục ./myweb thành thư mục /myweb trong nginx
- Mount file ./nginx/nginx.conf vào file /etc/nginx/nginx.conf trong nginx
<img width="727" height="673" alt="image" src="https://github.com/user-attachments/assets/fc553e45-47cd-442f-aa05-3c0e06151b9a" />
'''

'''
#### Edit file ./nginx/nginx.conf để: Cấu hình web server cổng 80 server_name là sub-domain (sub-domain tuỳ ý của em) location / trỏ tới root là thư mục /myweb location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered
<img width="521" height="396" alt="image" src="https://github.com/user-attachments/assets/d549b695-a686-44d5-9c02-b96ffe3e2c87" />
