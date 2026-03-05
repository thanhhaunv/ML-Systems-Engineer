# 🟦 PHASE 1 (Month 1–3)

## OBJECTIVE:

Build Single-Node Production ML Platform (Designed-to-Scale)

---

# 📆 MONTH 1 – Infrastructure & Backend Core

## 🎯 Month 1 Strategic Outcome

* VPS production-hardened
* Dockerized system
* Reverse proxy + HTTPS
* Logging structured
* PostgreSQL production-ready
* Data model cho Ad Event system
* Basic load test
* CI/CD baseline

---

## 🔵 SPRINT STRUCTURE (Month 1)

Month 1 = 2 Sprints
Each Sprint = 2 Weeks

---

# 🟦 SPRINT 1 – Production Infrastructure Layer (Week 1–2)

## 🎯 Sprint 1 Goal

Deploy a secure, observable, containerized backend publicly accessible over HTTPS.

---

## 🔹 Deliverables

* Hardened VPS
* Docker production stack
* FastAPI service
* Nginx reverse proxy
* HTTPS (auto renew)
* Structured logging
* Project repo structure
* Decision log + Risk log
* Sprint report

---

## 🔹 Engineering Scope

### 1️⃣ Security Baseline

* SSH key-only
* Root disabled
* Firewall rules
* Fail2ban (optional enhancement)

### 2️⃣ Containerization

* Multi-stage Docker build
* Compose-based stack
* Environment separation

### 3️⃣ API Layer

* Health endpoint
* Predict mock endpoint
* Versioned API prefix

### 4️⃣ Reverse Proxy

* Nginx config
* Rate limit
* Timeout config

### 5️⃣ HTTPS

* Certbot
* Auto renew strategy

### 6️⃣ Logging

* JSON structured logging
* Log rotation
* Log persistence volume

---

## 🔹 Sprint KPI

* Public URL live
* HTTPS active
* Logs visible
* At least 12 meaningful commits
* Decision log maintained

---

# 🟦 SPRINT 2 – Database & Data Modeling (Week 3–4)

## 🎯 Sprint 2 Goal

Design and optimize relational schema for Ad Event system with production-grade DB practices.

---

## 🔹 Deliverables

* PostgreSQL containerized
* Schema design (users, ads, events, clicks)
* Index strategy documented
* Query performance benchmark
* Basic load simulation
* Migration strategy
* ER diagram
* Query optimization report

---

## 🔹 Engineering Scope

### 1️⃣ PostgreSQL Production Setup

* Resource limits
* Volume persistence
* Backup strategy (logical dump)

### 2️⃣ Data Modeling

Entities:

* user
* ad
* campaign
* event (impression, click)
* conversion

Design:

* Primary keys
* Foreign keys
* Indexing
* Composite index strategy

### 3️⃣ Performance

* EXPLAIN ANALYZE
* Index tuning
* Write-heavy vs read-heavy tradeoff

### 4️⃣ Load Testing

* Simulate event insert
* Measure latency
* Observe CPU & memory

### 5️⃣ CI/CD Extension

* Auto build + deploy DB migration
* Basic GitHub Actions workflow

---

## 🔹 Sprint KPI

* Schema documented
* ER diagram committed
* Query < acceptable latency threshold
* Load test results logged
* Sprint retrospective written

---

# 📊 End of Month 1 – You Must Be Able To:

✔ Deploy backend public
✔ Secure Linux server
✔ Understand container runtime
✔ Design relational schema
✔ Optimize query
✔ Run basic load test
✔ Document architecture decisions

If not achieved → Phase 1 unstable.

---

Next descent level:

We move to **Month 2 Sprint Architecture**
(Streaming + ClickHouse layer)

Proceeding.
