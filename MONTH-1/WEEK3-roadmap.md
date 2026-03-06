Dưới đây là **Roadmap + Daily Plan cho Week 3** theo đúng format bootcamp như các tuần trước.
Mình giữ nguyên triết lý của roadmap bạn đã xây: **3h/ngày, học lý thuyết → thực hành → document → test**.

Tuần này cực kỳ quan trọng vì:

> **90% hệ thống data chết vì schema design tệ.**

---

# 📅 WEEK 3 – PostgreSQL Production Setup & Schema Design

> Chủ đề: **“Schema quyết định tương lai hệ thống”**

---

# 🎯 Week 3 Strategic Outcome

Sau tuần này bạn phải đạt được:

✔ PostgreSQL chạy production-style bằng Docker
✔ Database có **volume persistence**
✔ Schema cho **Ad Event System** hoàn chỉnh
✔ ER diagram rõ ràng
✔ Index strategy documented
✔ Backup + restore test thành công

---

# 🧠 Knowledge Targets

Bạn phải hiểu các concept sau.

## Relational Modeling

Các nguyên tắc:

```
entity
relationship
normalization
```

Ví dụ:

```
user
campaign
ad
event
conversion
```

---

## Primary Key Strategy

Hai lựa chọn phổ biến:

| Type   | Ưu điểm          | Nhược     |
| ------ | ---------------- | --------- |
| SERIAL | nhanh            | dễ đoán   |
| UUID   | distributed safe | index lớn |

Production system thường dùng:

```
UUID v4
```

---

## Index Fundamentals

Index giúp:

```
O(n) → O(log n)
```

Nhưng:

```
write cost ↑
disk ↑
```

Vì vậy **không index mọi thứ**.

---

## Query Plan

Postgres dùng **query planner** để chọn execution plan.

Tool quan trọng:

```
EXPLAIN ANALYZE
```

---

## Backup Strategy

Production phải có:

```
logical backup
restore test
```

Tool:

```
pg_dump
```

---

# 🛠 Implementation Scope

---

# 🐘 1️⃣ PostgreSQL Production Setup

Phải làm:

* PostgreSQL container
* Persistent volume
* Resource limit
* Basic tuning
* Backup script
* Restore test

---

## Deliverables

```
docker-compose.yml (updated)
scripts/backup.sh
docs/postgres-setup.md
```

---

# 🧩 2️⃣ Data Modeling – Ad Event System

Entities:

```
user
campaign
ad
event
conversion
```

---

## Relationship

```
user → event
campaign → ad
ad → event
event → conversion
```

---

## Deliverables

```
db/schema.sql
docs/data-model-design.md
docs/er-diagram.png
```

---

# ⚡ 3️⃣ Query Optimization

Phải làm:

* EXPLAIN ANALYZE
* test index
* benchmark query

---

## Deliverables

```
docs/query-benchmark.md
```

---

# 📆 WEEK 3 DAILY PLAN (3h/day)

---

# 🟢 Day 1 — PostgreSQL Architecture Fundamentals

## ⏱ Time Split

```
Theory      70m
Hands-on    80m
Review      30m
```

---

## 📚 Knowledge

Hiểu PostgreSQL architecture:

```
Client
 ↓
Connection
 ↓
Query Parser
 ↓
Planner
 ↓
Executor
 ↓
Storage Engine
```

---

### PostgreSQL Storage

Database structure:

```
database
  └ tables
      └ rows
```

Storage engine:

```
heap table
index
WAL (write ahead log)
```

---

### WAL Concept

Write Ahead Log đảm bảo:

```
durability
crash recovery
```

---

## 🛠 Practice

Run PostgreSQL container.

docker-compose update:

```yaml
postgres:
  image: postgres:15
  environment:
    POSTGRES_USER: app
    POSTGRES_PASSWORD: password
    POSTGRES_DB: ad_platform
  volumes:
    - pgdata:/var/lib/postgresql/data
```

Test:

```
docker compose up
```

---

## 📦 Deliverable

```
docs/postgres-architecture.md
```

---

# 🟢 Day 2 — PostgreSQL Production Container Setup

## 📚 Knowledge

Hiểu:

### Resource Limits

Container không nên unlimited.

Example:

```
CPU limit
RAM limit
```

---

### Persistence

Nếu không mount volume:

```
container restart → data mất
```

---

## 🛠 Practice

docker-compose:

```yaml
services:

  postgres:
    image: postgres:15
    restart: always

    volumes:
      - pgdata:/var/lib/postgresql/data

    ports:
      - "5432:5432"
```

---

Test persistence:

```
insert row
restart container
check data
```

---

## 📦 Deliverables

```
docs/postgres-container-setup.md
```

---

# 🟢 Day 3 — Schema Design Fundamentals

## 📚 Knowledge

Hiểu **normalization**.

Example:

Bad design:

```
event table chứa user_name
```

Good design:

```
user table
event table
```

---

### Entity Identification

Ad platform cần:

```
user
campaign
ad
event
conversion
```

---

### Event Types

```
impression
click
conversion
```

---

## 🛠 Practice

Design schema:

```
users
campaigns
ads
events
conversions
```

---

Example event table:

```sql
CREATE TABLE events (

 id UUID PRIMARY KEY,
 user_id UUID,
 ad_id UUID,
 event_type TEXT,
 created_at TIMESTAMP
);
```

---

## 📦 Deliverables

```
db/schema.sql
docs/data-model-design.md
```

---

# 🟢 Day 4 — ER Diagram

## 📚 Knowledge

ER diagram giúp:

```
visualize relationship
avoid schema mistake
```

---

Relationship example:

```
User → Event
Campaign → Ad
Ad → Event
Event → Conversion
```

---

## 🛠 Practice

Dùng tool:

```
draw.io
dbdiagram.io
```

---

Example:

```
user 1----* event
ad 1----* event
campaign 1----* ad
```

---

## 📦 Deliverables

```
docs/er-diagram.png
```

---

# 🟢 Day 5 — Index Strategy

## 📚 Knowledge

Index types:

```
B-tree (default)
Hash
GIN
```

---

Most queries:

```
events by user
events by ad
events by time
```

---

Index example:

```sql
CREATE INDEX idx_event_user
ON events(user_id);
```

Composite index:

```sql
CREATE INDEX idx_event_user_time
ON events(user_id, created_at);
```

---

## 🛠 Practice

Test query speed:

```
without index
with index
```

---

## 📦 Deliverables

```
docs/index-strategy.md
```

---

# 🟢 Day 6 — Backup & Restore

## 📚 Knowledge

Production rule:

```
backup chưa test restore = backup vô nghĩa
```

---

### Logical Backup

Tool:

```
pg_dump
```

---

Backup:

```
pg_dump -U app ad_platform > backup.sql
```

---

Restore:

```
psql -U app ad_platform < backup.sql
```

---

## 🛠 Practice

Viết script:

```
scripts/backup.sh
```

Example:

```bash
#!/bin/bash

pg_dump -U app ad_platform > backup_$(date +%F).sql
```

---

## 📦 Deliverables

```
scripts/backup.sh
docs/backup-restore-test.md
```

---

# 🟢 Day 7 — Query Optimization

## 📚 Knowledge

Tool quan trọng:

```
EXPLAIN ANALYZE
```

---

Example:

```sql
EXPLAIN ANALYZE
SELECT *
FROM events
WHERE user_id = '123';
```

---

Bạn sẽ thấy:

```
Seq Scan
Index Scan
Execution Time
```

---

## 🛠 Practice

Test:

```
no index
index
compare latency
```

---

## 📦 Deliverables

```
docs/query-benchmark.md
```

---

# 📊 Week 3 KPI

Bạn đạt:

✔ PostgreSQL container chạy ổn định
✔ Volume persistence hoạt động
✔ Schema thiết kế hoàn chỉnh
✔ ER diagram commit
✔ Index strategy documented
✔ Backup + restore test pass

---

# 📂 Repo Structure After Week 3

```
app/
docker/
infra/
docs/
db/
scripts/

logs/
.github/workflows/
```

---

# 🚀 Sau Week 3 bạn sẽ đạt level

**Junior Backend/Data Engineer**

Bạn sẽ hiểu:

```
database architecture
data modeling
index strategy
query optimization
backup strategy
```

Đây là nền tảng của:

* Data Engineering
* ML pipeline
* Analytics system
* Ad tech platform

---

Nếu bạn muốn, bước tiếp theo mình sẽ viết luôn:

**Week 4 Roadmap (Load Testing + Migration + CI/CD DB Automation)**

Tuần này là **điểm bắt đầu của tư duy Data Engineer thực thụ**, vì nó bắt đầu chạm tới:

* **write throughput**
* **event ingestion**
* **schema evolution**.
