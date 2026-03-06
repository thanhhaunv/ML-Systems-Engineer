Rồi. Breakdown Month 1 xuống **mức tuần**.
Không hỏi gì thêm. Làm đúng kiểu production bootcamp.

---

# 📆 MONTH 1 – Infrastructure & Backend Core

(4 tuần – 3h/ngày)

---

# 🟦 SPRINT 1 – Production Infrastructure Layer

(Week 1–2)

---

# 📅 WEEK 1 – Secure VPS + Container Foundation

> Chủ đề: “Không secure thì đừng deploy”

---

## 🎯 Week 1 Outcome

* VPS hardened
* Docker production-ready
* FastAPI container chạy được
* Logging structured
* Repo structure chuẩn
* Decision log bắt đầu

---

## 🔹 Focus Breakdown

### 🔐 1️⃣ Linux Production Hardening

Bạn phải thực hiện:

* SSH key-only authentication
* Disable password login
* Disable root login
* Change SSH port (optional)
* UFW firewall (allow 22/80/443 only)
* Fail2ban (optional but recommended)
* Auto security updates

Deliverable:

* `security-checklist.md`
* Screenshot hoặc log xác nhận config

---

### 🐳 2️⃣ Docker Production Foundation

Phải làm:

* Install Docker + Docker Compose
* Tạo multi-stage Dockerfile cho FastAPI
* Tách `requirements.txt`
* .env management
* Non-root container user
* Healthcheck trong Dockerfile

Deliverable:

* `Dockerfile`
* `docker-compose.yml`
* `env.example`

---

### 🧱 3️⃣ FastAPI Minimal Production API

Phải có:

* `/health`
* `/api/v1/predict` (mock)
* Versioned prefix
* Structured JSON logging
* Request ID middleware

Deliverable:

* API chạy trong container
* Log ra JSON format

---

### 📂 4️⃣ Project Structure

Phải có:

```
app/
docker/
infra/
docs/
logs/
.github/workflows/
```

Deliverable:

* Repo commit structure rõ ràng
* Ít nhất 6–8 commit meaningful tuần này

---

## 📊 Week 1 KPI

✔ SSH password login disabled
✔ Container chạy OK
✔ Logs JSON format
✔ Health endpoint OK
✔ Repo clean

---

---

# 📅 WEEK 2 – Reverse Proxy + HTTPS + Observability Base

> Chủ đề: “Public but controlled”

---

## 🎯 Week 2 Outcome

* Public domain live
* HTTPS auto-renew
* Reverse proxy config chuẩn
* Rate limiting
* Log persistence
* Sprint report viết xong

---

## 🔹 Focus Breakdown

### 🌐 1️⃣ Nginx Reverse Proxy

Phải cấu hình:

* Proxy pass to FastAPI
* Timeout config
* Buffer config
* Rate limiting
* Basic security headers

Deliverable:

* `nginx.conf`
* Config explanation document

---

### 🔒 2️⃣ HTTPS Production Setup

Phải làm:

* Domain pointing
* Certbot SSL
* Auto-renew cron
* Test renewal

Deliverable:

* HTTPS verified
* Renewal test log

---

### 📊 3️⃣ Logging Persistence

* Mount volume logs
* Log rotation
* Error vs Access log separation
* Test restart → logs không mất

---

### 🧾 4️⃣ Engineering Documentation

Bạn phải viết:

* Decision log
* Risk log
* Sprint 1 retrospective
* Architecture v1 diagram

---

## 📊 Week 2 KPI

✔ Public URL live
✔ HTTPS active
✔ Rate limit working
✔ Log rotation working
✔ Sprint report committed

---

# 🟦 SPRINT 2 – Database & Data Modeling

(Week 3–4)

---

# 📅 WEEK 3 – PostgreSQL Production Setup & Schema Design

> Chủ đề: “Schema quyết định tương lai hệ thống”

---

## 🎯 Week 3 Outcome

* PostgreSQL containerized
* Volume persistence
* ER diagram hoàn chỉnh
* Index strategy documented

---

## 🔹 Focus Breakdown

### 🐘 1️⃣ PostgreSQL Production Setup

Phải làm:

* Resource limit
* Volume mapping
* Basic config tuning
* Logical backup script
* Restore test

Deliverable:

* `backup.sh`
* Restore demo

---

### 🧩 2️⃣ Data Modeling – Ad Event System

Entities:

* user
* ad
* campaign
* event (impression, click)
* conversion

Phải xác định:

* Primary key strategy (UUID vs serial)
* Foreign key relationship
* Composite index
* Partition strategy (optional advanced)

Deliverable:

* `schema.sql`
* ER diagram PNG
* Design document

---

### ⚡ 3️⃣ Query Optimization

Phải làm:

* EXPLAIN ANALYZE
* Index test
* Compare before/after
* Document latency

Deliverable:

* Query benchmark report

---

## 📊 Week 3 KPI

✔ Schema complete
✔ ER diagram committed
✔ Index strategy documented
✔ Backup test successful

---

---

# 📅 WEEK 4 – Load Simulation + CI/CD Baseline

> Chủ đề: “Test before trust”

---

## 🎯 Week 4 Outcome

* Event insert simulation
* Basic load test report
* GitHub Actions CI/CD working
* Migration strategy defined

---

## 🔹 Focus Breakdown

### 🚀 1️⃣ Load Simulation

Phải simulate:

* 1k insert
* 10k insert
* Concurrent insert

Đo:

* Latency
* CPU
* Memory

Deliverable:

* Load test report
* Screenshot monitoring

---

### 🔄 2️⃣ Migration Strategy

* Versioned SQL migration
* Rollback script
* Migration folder structure

Deliverable:

* Migration plan document

---

### 🔁 3️⃣ CI/CD Baseline

GitHub Actions phải:

* Build Docker image
* Run test
* Push image
* Deploy to VPS (simple SSH deploy)

Deliverable:

* `.github/workflows/deploy.yml`

---

### 🧾 4️⃣ Sprint 2 Retrospective

Phải viết:

* What worked
* Bottleneck
* Technical debt
* Improvement plan

---

## 📊 Week 4 KPI

✔ Load test complete
✔ Migration tested
✔ CI/CD deploy successful
✔ Sprint report written

---

# 📊 END OF MONTH 1 CHECKLIST

Bạn phải tự tin trả lời:

* Làm sao secure VPS?
* Docker multi-stage để làm gì?
* Reverse proxy xử lý gì?
* Vì sao cần structured logging?
* Khi nào cần composite index?
* EXPLAIN ANALYZE đọc thế nào?
* Backup PostgreSQL ra sao?
* Nếu DB chết thì xử lý sao?

---

Nếu không trả lời trôi chảy →
Month 2 không được bắt đầu.

---

Giờ ta tiếp tục:

🔹 Breakdown từng tuần thành **Daily 3h blocks**
hay
🔹 Sang luôn breakdown Month 2 Weeks?
