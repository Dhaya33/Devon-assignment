 Nginx Reverse Proxy with Docker Compose

This project demonstrates how to containerize two backend microservices — one built with Golang and another with Python Flask — and route them through an Nginx reverse proxy, all orchestrated using Docker Compose.

---

## 📁 Project Structure

├── docker-compose.yml # Compose file to orchestrate all services
├── nginx/
│ ├── nginx.conf # Nginx reverse proxy configuration
│ └── Dockerfile # Dockerfile for Nginx container
├── service_1/ # Golang backend service
│ ├── main.go
│ └── Dockerfile
├── service_2/ # Python Flask backend service
│ ├── app.py
│ ├── requirements.txt
│ └── Dockerfile
└── README.md


---

## ⚙️ Services Overview

| Service     | Tech Stack     | URL Path Prefix | Port Inside Container |
|-------------|----------------|------------------|------------------------|
| Service 1   | Golang         | `/service1/`     | `8001`                 |
| Service 2   | Python + Flask | `/service2/`     | `8082`                 |
| Nginx       | Nginx          | Reverse Proxy    | `80`                   |

---

## 🔁 Nginx Routing Rules

Nginx forwards requests as follows:

- `/service1/*` ⟶ Golang app at `service_1:8001`
- `/service2/*` ⟶ Flask app at `service_2:8082`

Incoming requests are also logged with timestamps and paths for visibility.

---

## 🚀 How to Run

### Prerequisites

- Docker
- Docker Compose

### Run all services with a single command:

bash
$ docker-compose up --build
------------------------------
Access Services in Browser
http://localhost:8080/service1/ping
http://localhost:8080/service1/hello
http://localhost:8080/service2

--------------------------------
 Health Checks

Both services have health checks configured in docker-compose.yml:

service_1 is healthy if /ping returns 200 OK
service_2 is healthy if / returns 200 OK
Check status with:

$ docker ps

---------------------------------
 Logs

To view real-time logs:

docker-compose logs -f
docker-compose logs nginx
docker-compose logs service_1
docker-compose logs service_2

---------------------------------
Use curl for quick API checks:

curl http://localhost:8080/service1/hello
curl http://localhost:8080/service2
