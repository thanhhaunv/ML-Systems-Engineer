Tốt. Trước khi viết nội dung chi tiết, chúng ta cần **Roadmap của MONTH 1 thật rõ ràng** để tránh loạn khi đi vào từng bài.

Tôi sẽ thiết kế **ROADMAP theo đúng tinh thần bootcamp quân đội**:

* rõ mục tiêu
* rõ skill
* rõ deliverable
* rõ bài thực hành
* rõ hệ thống cuối tháng

---

# 🟦 MONTH 1 ROADMAP

## Production Infrastructure & Backend Core

**Duration**

```
4 weeks
~3h/day
~84 hours total
```

---

# 🎯 MONTH 1 MISSION

Xây **production server thật** có thể deploy backend service.

Không còn kiểu:

```
python main.py
```

Mà là:

```
Internet
 → HTTPS
 → Reverse Proxy
 → Docker
 → FastAPI
 → PostgreSQL
```

Hệ thống chạy trên **VPS thật**.

---

# 🧠 SKILL TARGET

Sau tháng 1 bạn phải thành thạo:

| Skill               | Level            |
| ------------------- | ---------------- |
| Linux production    | intermediate     |
| SSH security        | solid            |
| Docker              | production usage |
| Docker Compose      | production stack |
| Nginx reverse proxy | confident        |
| TLS / HTTPS         | confident        |
| PostgreSQL          | intermediate     |
| FastAPI backend     | production ready |
| Logging             | structured       |
| Load testing        | basic            |

---

# 🧱 FINAL SYSTEM (END OF MONTH)

Kiến trúc cuối tháng:

```
Internet
   │
   ▼
Nginx Reverse Proxy
   │
   ▼
Docker Network
   │
   ├── FastAPI Container
   │
   └── PostgreSQL Container
```

API endpoint:

```
POST /ad/impression
```

Hệ thống ghi **ad events vào database**.

---

# 🗓 WEEK STRUCTURE

```
Week 1
Infrastructure foundation
```

```
Week 2
Production server setup
```

```
Week 3
Backend architecture
```

```
Week 4
Database + API production
```

---

# 🪖 WEEK 1

# Infrastructure Foundation

## Objective

Hiểu **Linux production environment**.

Không học kiểu:

```
copy paste tutorial
```

Mà hiểu:

```
server
process
network
container
```

---

## Theory

```
Linux filesystem
User permission
Process management
Networking basics
Ports
Package management
Docker concept
Container vs VM
```

---

## Labs

```
SSH into server
Basic Linux commands
Install packages
Manage users
Explore system logs
Run first docker container
```

---

## Outcome

Bạn hiểu:

```
server hoạt động thế nào
container là gì
docker làm gì
```

---

# 🪖 WEEK 2

# Production Server Setup

## Objective

Biến VPS thành **production server an toàn**.

---

## Theory

```
SSH security
Key authentication
Firewall concept
Fail2ban
TLS / HTTPS
Reverse proxy
```

---

## Labs

```
Disable root login
Disable password login
Enable SSH key auth
Setup UFW firewall
Install Fail2ban
Install Docker
Install Docker Compose
Deploy Nginx container
Setup HTTPS
```

---

## Outcome

Server đạt chuẩn:

```
SSH secured
Firewall enabled
HTTPS enabled
Docker platform ready
```

---

# 🪖 WEEK 3

# Backend Core Architecture

## Objective

Xây **backend production skeleton**.

---

## Theory

```
REST API design
Service layer
Dependency injection
Configuration management
Environment variables
Logging strategy
```

---

## Labs

Create project structure:

```
backend/
 ├── api
 ├── services
 ├── models
 ├── schemas
 ├── config
 └── main.py
```

Implement:

```
FastAPI app
health endpoint
config loader
logging system
```

---

## Outcome

API server chạy trong **Docker container**.

---

# 🪖 WEEK 4

# Database & Event Modeling

## Objective

Thiết kế **database cho ad tracking system**.

---

## Theory

```
PostgreSQL architecture
Indexes
Query planner
Connection pooling
Data modeling
Event schema
```

---

## Labs

Install stack:

```
PostgreSQL
SQLAlchemy
Alembic
```

Create table:

```
ad_event
```

Fields:

```
event_id
user_id
ad_id
zone_id
website_id
timestamp
device
ip
```

---

## Build API

```
POST /ad/impression
```

Flow:

```
Client
 → API
 → Insert event
 → PostgreSQL
```

---

## Load test

Simulate:

```
1000 req/sec
```

---

# 🧪 FINAL MINI PROJECT

Deploy:

```
FastAPI + PostgreSQL
```

through:

```
Internet
 → HTTPS
 → Nginx
 → Docker
 → API
```

Test endpoint:

```
https://api.domain.com/ad/impression
```

---

# 📦 DELIVERABLES (END OF MONTH)

Repository phải có:

```
backend/
docker-compose.yml
nginx/
docs/
```

Server chạy:

```
FastAPI
PostgreSQL
Nginx
Docker
```

---

# 📈 SKILL LEVEL AFTER MONTH 1

Bạn sẽ vượt qua **80% dev junior** ở điểm:

```
biết deploy production system
```

chứ không chỉ:

```
viết code
```

---

# 📌 NEXT STEP

Sau roadmap này chúng ta sẽ tạo tiếp:

```
MONTH 1 STRUCTURE
```

cụ thể:

```
Part 1
Infrastructure Foundation

Part 2
Production Server Setup

Part 3
Backend Core

Part 4
Database & Event Modeling
```

---

Nếu bạn muốn, bước tiếp theo tôi sẽ viết luôn:

**ROADMAP.md chuẩn production cho repository**
(viết kiểu **GitHub project readme rất đẹp và chuyên nghiệp**) — thứ mà sau này **recruiter nhìn vào là thấy ngay level của bạn.**
