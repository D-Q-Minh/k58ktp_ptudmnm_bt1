# E. Triển khai (level test) ứng dụng
#### 
- Chuyển vào trong thư mục ~/myapp
- Gõ lệnh để docker compose chạy: sẽ run tất cả các service khai báo trong file docker-compose.yml
- Lợi ích: Chỉ cần docker-compose up -d là toàn bộ hệ thống (Web + Node-RED + Tunnel) tự chạy
- Trước hết, ta thêm cloudflared trong docker-compose.yml:

<img width="1352" height="182" alt="image" src="https://github.com/user-attachments/assets/acd3e15d-2a1f-43f6-b565-09ecbeead633" />

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

  cloudflared:
    image: cloudflare/cloudflared:latest
    container_name: cloudflared-tunnel_k3y4_bt1
    restart: unless-stopped
    command: tunnel --no-autoupdate run --token eyJhIjoiMzljZDJiMmQyNDNhZDU3MzA2ZjFjMGY0OTA5ZTZlYWIiLCJ0IjoiODZjMDViNjktZGE4My00OTFjLWFmMmYtZjE3YTcwZGEyZTRjIiwicyI6IlpHUmtOemM0TW1VdFlUZGhNQzAwT1dWaExXSmtNV0V0TTJaa01qWTRObUkyWm1VeCJ9
    networks:
      - my-network

# Khai báo mạng chung để các container giao tiếp với nhau
networks:
  my-network:
    driver: bridge
```
