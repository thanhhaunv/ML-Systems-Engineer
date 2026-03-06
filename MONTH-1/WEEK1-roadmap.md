Rất đúng. Cách chuẩn nhất là:

```
ROADMAP (Week)
 ├── Daily Plan
 │     ├── Knowledge
 │     ├── Implementation
 │     ├── Deliverables
 │     └── Exercises
 └── Final Test
```

Sau đó **lesson thật sẽ viết theo từng Day**.

Như vậy roadmap sẽ **không bị mơ hồ** và lesson sẽ **không bị lan man**.

Dưới đây là **WEEK 1 ROADMAP hoàn chỉnh + DAILY PLAN (3h/ngày)**.

---

# 📅 WEEK 1 – Secure VPS + Container Foundation

> Chủ đề: **“Không secure thì đừng deploy”**

---

# 🎯 Week 1 Strategic Outcome

Sau tuần này bạn phải:

✔ VPS hardened
✔ Docker production-ready
✔ FastAPI container chạy được
✔ Logging structured
✔ Repo structure chuẩn
✔ Decision log bắt đầu

---

# 🧠 Knowledge Targets

Bạn phải **hiểu được các concept sau**:

### Linux Server

* Linux user model
* File permissions
* Process & services
* Systemctl basics

### Server Security

* SSH authentication
* Public key cryptography
* Firewall concept
* Brute force attack

### Docker

* Container vs VM
* Docker image layers
* Container lifecycle
* Docker networking basics

### Backend API

* REST endpoint
* API versioning
* Middleware
* Structured logging

---

# 🛠 Implementation Scope

## 🔐 Linux Production Hardening

Bạn phải thực hiện:

* SSH key-only authentication
* Disable password login
* Disable root login
* Change SSH port (optional)
* UFW firewall (allow 22/80/443 only)
* Fail2ban (optional but recommended)
* Auto security updates

Deliverable:

```
docs/security-checklist.md
```

---

## 🐳 Docker Production Foundation

Phải làm:

* Install Docker + Docker Compose
* Tạo multi-stage Dockerfile cho FastAPI
* Tách `requirements.txt`
* `.env` management
* Non-root container user
* Healthcheck trong Dockerfile

Deliverables:

```
Dockerfile
docker-compose.yml
env.example
```

---

## 🧱 FastAPI Minimal Production API

Phải có:

```
/health
/api/v1/predict
```

Features:

* Versioned prefix
* Structured JSON logging
* Request ID middleware

Deliverable:

API chạy trong container.

---

## 📂 Project Structure

Repo phải có:

```
app/
docker/
infra/
docs/
logs/
.github/workflows/
```

Deliverable:

Repo commit structure rõ ràng.

---

# 📆 WEEK 1 DAILY PLAN (3h/day)

---

# 🟢 Day 1 — Linux Server Fundamentals

## ⏱ Time Split

```
Theory      60m
Hands-on    90m
Review      30m
```

---

## 📚 Knowledge

Hiểu:

### Linux User Model

```
root
user
sudo
```

Vì sao **không dùng root cho production**.

---

### File Permission

Hiểu:

```
rwx
chmod
chown
```

---

### Process Basics

Commands:

```
ps
top
systemctl
```

---

## 🛠 Practice

Trên VPS:

```
adduser deploy
usermod -aG sudo deploy
```

Test:

```
sudo whoami
```

---

## 📦 Deliverable

File:

```
docs/linux-basics.md
```

---

# 🟢 Day 2 — Server Security Hardening

## 📚 Knowledge

Hiểu:

### SSH Authentication

2 loại:

```
password
key-based
```

Production:

```
key-based only
```

---

### Firewall Concept

Hiểu:

```
port
ingress
egress
```

---

### Brute Force Attack

Bot scan internet.

Solution:

```
fail2ban
```

---

## 🛠 Practice

Thực hiện:

```
ssh-keygen
```

Upload key.

Disable password login.

Edit:

```
/etc/ssh/sshd_config
```

```
PasswordAuthentication no
PermitRootLogin no
```

---

Enable firewall:

```
ufw allow 22
ufw allow 80
ufw allow 443
ufw enable
```

---

## 📦 Deliverable

```
docs/security-checklist.md
```

---

# 🟢 Day 3 — Docker Fundamentals

## 📚 Knowledge

Hiểu:

### Container vs VM

VM:

```
full OS
```

Container:

```
isolated process
```

---

### Docker Architecture

Components:

```
docker client
docker daemon
image
container
registry
```

---

### Docker Image Layer

Image = nhiều **filesystem layers**.

---

## 🛠 Practice

Install Docker:

```
docker --version
```

Run container:

```
docker run hello-world
```

---

## 📦 Deliverable

```
docs/docker-basics.md
```

---

# 🟢 Day 4 — Dockerfile + Compose

## 📚 Knowledge

Hiểu:

### Dockerfile

Commands:

```
FROM
COPY
RUN
CMD
```

---

### Multi-stage Build

Mục tiêu:

```
reduce image size
```

---

### Docker Compose

Use when:

```
multi-container system
```

---

## 🛠 Practice

Tạo:

```
Dockerfile
docker-compose.yml
```

Build:

```
docker compose up
```

---

## 📦 Deliverables

```
Dockerfile
docker-compose.yml
```

---

# 🟢 Day 5 — FastAPI Production API

## 📚 Knowledge

Hiểu:

### REST Endpoint

Example:

```
GET /health
POST /predict
```

---

### API Versioning

Example:

```
/api/v1
/api/v2
```

---

### Structured Logging

Text log:

```
User login success
```

JSON log:

```
{
  "event": "login",
  "user_id": 123
}
```

Production:

```
JSON logs
```

---

## 🛠 Practice

FastAPI app:

```
/health
/api/v1/predict
```

Run container.

---

## 📦 Deliverables

```
app/main.py
```

---

# 🟢 Day 6 — Integration & Deploy

## 🎯 Goal

Deploy **FastAPI container lên VPS**.

---

## Tasks

Run:

```
docker compose up -d
```

Test:

```
curl localhost:8000/health
```

---

Check logs:

```
docker logs
```

---

## 📦 Deliverables

Working API container.

---

# 🟢 Day 7 — Review + Test

## 🧪 Theory Test

Giải thích:

1️⃣ Docker vs VM
2️⃣ SSH key authentication
3️⃣ firewall hoạt động thế nào
4️⃣ structured logging

---

## 🧪 Practical Test

Server phải chạy:

```
curl localhost:8000/health
```

Response:

```
200 OK
```

---

# 📊 Week 1 KPI

Bạn đạt:

✔ SSH password disabled
✔ Docker container chạy
✔ FastAPI container running
✔ JSON logs working
✔ Repo structure clean

---

# 📂 Repo Expected Structure

```
project-root

app/
docker/
infra/
docs/
logs/

.github/workflows/
```

---

# 🧠 Engineering Habit (bắt buộc)

Tạo file:

```
docs/decision-log.md
```

Example:

```
ADR-001
Use Docker Compose instead of Kubernetes
Reason: simplicity
```

---

# 🚀 Nếu bạn đi đúng roadmap này

Sau **7 ngày** bạn sẽ:

* biết **harden server**
* biết **containerize API**
* hiểu **production basics**

Đây chính là **foundation của DevOps / MLOps / Platform Engineering**.

---

Nếu bạn muốn, bước tiếp theo mình sẽ viết:

# 📚 Day 1 Lesson – Linux Production Fundamentals

(theo chuẩn **mini DevOps bootcamp**, đọc ~20 phút + lab ~90 phút)

Phần đó sẽ giúp bạn **hiểu Linux như production engineer**, không phải kiểu tutorial.
