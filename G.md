# G. Triển khai ứng dụng đến End-user
#### Tạo tunnel (đường hầm)
##### Trước hết cần cài cloudflared:
##### <img width="468" height="41" alt="da cai cloudflared tren docker" src="https://github.com/user-attachments/assets/1ee16457-fa63-406f-9490-798e22f70519" />
<img width="468" height="41" alt="da cai cloudflared tren docker" src="https://github.com/user-attachments/assets/6106ddcc-d55a-4ea2-a3b5-808898363b19" />

#### Tiếp theo là tạo Tunnel:(dùng Remote-Managed)
##### Cách này thì đơn giản vì tạo tunnel bằng Web cloudflared có UI và hướng dẫn, chỉ cần dùng token, không cần config.yml và file (tunnelID).json

##### Bước 1: Tạo tunnel. Vào Networking==>Tunnels==>Create Tunnel:
<img width="856" height="535" alt="tạo tunnel ,0" src="https://github.com/user-attachments/assets/9172c06d-7b65-40b0-8972-df4692099b69" />
<img width="454" height="476" alt="tạo tunnel ,1" src="https://github.com/user-attachments/assets/37ace20f-fb36-449b-8c10-5a78e7bb9ba7" />
<img width="1064" height="425" alt="tạo tunnel ,2 - Screenshot 2026-04-13 220521" src="https://github.com/user-attachments/assets/b14673af-9d1d-4177-b979-9f5d49fa0a14" />

##### Bước 2: Copy dòng lệnh màu cam, paste vào Ubuntu (tại vị trí ~/myapp)
<img width="1030" height="537" alt="tạo tunnel ,3" src="https://github.com/user-attachments/assets/9bc96b1c-4dc7-4306-8188-99cbd9dc970a" />
<img width="1363" height="392" alt="tạo tunnel ,3 1" src="https://github.com/user-attachments/assets/e3624c6f-68ab-4df0-b5c9-f4dbdf2b94ce" />

##### Bước 3: Convert sang docker-compose
```
cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared-tunnel_k3y4_bt1
    restart: unless-stopped
    command: tunnel --no-autoupdate run --token eyJhIjoiMzljZDJiMmQyNDNhZDU3MzA2ZjFjMGY0OTA5ZTZlYWIiLCJ0IjoiODZjMDViNjktZGE4My00OTFjLWFmMmYtZjE3YTcwZGEyZTRjIiwicyI6IlpHUmtOemM0TW1VdFlUZGhNQzAwT1dWaExXSmtNV0V0TTJaa01qWTRObUkyWm1VeCJ9
    networks:
      - my-network
```
<img width="1030" height="135" alt="image" src="https://github.com/user-attachments/assets/19244236-af61-4fb0-a73d-7e4d4cd3150d" />

##### Bước 4: Cấu hình Public Hostname
<img width="542" height="497" alt="tạo tunnel ,4" src="https://github.com/user-attachments/assets/8811c73f-1a2c-46c8-a69c-8c808ac17424" />
<img width="1114" height="64" alt="tạo tunnel ,5" src="https://github.com/user-attachments/assets/8506a685-9bd2-4d09-8b12-e266fd2b47b6" />

##### Bước 5: Cấu hình lại nginx.conf
```
events { worker_connections 1024; }

http {
    include /etc/nginx/mime.types;
    default_type application/octet-stream;

    server {
        listen 80;
        server_name tnut58ktp047.id.vn;

        location / {
            root /myweb;
            index index.html;
        }

        location /api/ {
            proxy_pass http://nodered:1880/;
			proxy_set_header Host $host;
			proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```
##### Chạy lại docker compose
<img width="418" height="96" alt="docker compose up -d (co cloudflared)" src="https://github.com/user-attachments/assets/6d80b5f5-cacc-4d92-a1b1-3655ea43cbf8" />


## CẬP NHẬT:
###### hạn nộp bài, em kiểm tra nhưng web không lên
###### sau kiểm tra lại thì web đã lên, kiểm tra thiết bị sử dụng mạng khác đã vào được web
<img width="460" height="436" alt="image" src="https://github.com/user-attachments/assets/c0e39469-5877-4bb6-918c-0ccf1768ac95" />
