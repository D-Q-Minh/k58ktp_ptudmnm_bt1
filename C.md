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
```
services:
  nodered:
    image: nodered/node-red:latest
    container_name: nodered_k3y4_bt1
    ports:
      - "1880:1880"
    volumes:
      - ./nodered:/data
    # Healthcheck để đảm bảo Node-RED chạy ổn định trước khi các dịch vụ khác khởi động
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:1880/"]
      interval: 30s
      timeout: 10s
      retries: 3
    deploy:
      resources:
        limits:
          memory: 512M
    restart: unless-stopped
    networks:
      - my-network
  
  myapi:
    image: alpine:latest  # Thay thế 'build: ./myapi'
    container_name: myapi_k3y4_bt1
    ports:
      - "9630:9630"
      
  nginx:
    image: nginx:alpine
    container_name: nginx_k3y4_bt1
    ports:
      - "81:80"
    volumes:
      - ./myweb:/myweb:ro
      - ./nginx/nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      nodered:
        condition: service_healthy
    restart: unless-stopped
    networks:
      - my-network
```
#### Edit file ./nginx/nginx.conf để: Cấu hình web server cổng 80 server_name là sub-domain (sub-domain tuỳ ý của em) location / trỏ tới root là thư mục /myweb location /api dùng proxy_pass trỏ tới 1 (hoặc nhiều) node http_in của nodered
<img width="521" height="396" alt="image" src="https://github.com/user-attachments/assets/d549b695-a686-44d5-9c02-b96ffe3e2c87" />

#### Edit file ./nodered/settings.js để nodered bắt buộc đăng nhập
<img width="604" height="325" alt="dang nhap node red (da cai mk)" src="https://github.com/user-attachments/assets/14173108-3e25-4688-a826-9d1da4764407" />

- cập nhật file setting.js:
<img width="611" height="167" alt="image" src="https://github.com/user-attachments/assets/8e7b35e6-fc1f-4183-a8fd-7c04c02727fd" />

 #### kết quả phần C:
<img width="256" height="215" alt="image" src="https://github.com/user-attachments/assets/7e285d42-d890-4c8f-925f-eddd88c48d45" />

<img width="1120" height="333" alt="image" src="https://github.com/user-attachments/assets/9b4560e9-5e50-4799-b0c5-c3160347ed85" />
