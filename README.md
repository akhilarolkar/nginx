🌐 Nginx Server + Reverse Proxy + Load Balancer with HTTPS

This project demonstrates how to set up Nginx as a static file server, reverse proxy, and load balancer with HTTPS redirect.
There are 2 backend containers and 1 nginx container created using docker-compose file.

Features: \
Static file serving → from /frontend/index.html \
Reverse proxy → /api/ requests are forwarded to backend services \
Load balancing → Nginx alternates between backend1 and backend2 containers \
HTTPS enabled → with self-signed certificate

📂 Project Structure
. \
├── docker-compose.yml #to run nginx and backend containers \
├── nginx.conf #nginx configuration file \
├── frontend/ \
│   └── index.html \
├── ssl/ \
│   ├── server.crt \
│   └── server.key 

STEPS TO RUN THE PROJECT

### 1) Clone this repo.
### 2) Generate self-signed SSL certificates. Run inside the ssl folder using git bash terminal:  
Generate private key : \
openssl genrsa -out server.key 2048 \
Generate self-signed certificate (valid for 1 year) : \
openssl req -new -x509 -key server.key -out server.crt -days 365 -subj "//CN=localhost"

This creates: \
server.key → private key \
server.crt → certificate

### 3) Open Docker Desktop.

### 4) Start services with Docker Compose.
docker compose up -d --build

This will start:

backend1 → responds with “Hello from backend1” \
backend2 → responds with “Hello from backend2” \
nginx → serves static site + reverse proxies /api/

### 5) Access the application.
🌍 HTTP: http://localhost  will be auto redirected to -> 🔒 HTTPS: https://localhost

⚠️ Since the certificate is self-signed, your browser will show a security warning. You can safely proceed for local testing.

refresh https://localhost/api/ multiple times to check load balaning between backend1 & backend2

### 6) Stopping Services
docker compose down
