Dưới đây là **Roadmap + Daily Plan cho Week 4** theo đúng format các tuần trước, đảm bảo:

* học **lý thuyết cốt lõi → thực hành ngay**
* **3h/ngày**
* cuối tuần có **test nhiều cấp độ**
* giống **mini DevOps / Platform Engineering bootcamp**

Week này rất quan trọng vì nó dạy **engineering mindset**:

> *“System chưa test load thì chưa phải production.”*

---

# 📅 WEEK 4 – Load Simulation + CI/CD Baseline

> Chủ đề: **“Test before trust”**

---

# 🎯 Week 4 Outcome

Sau tuần này bạn phải đạt được:

* Simulate traffic cho hệ thống ad events
* Biết đo **DB performance**
* Biết **load test API**
* CI/CD pipeline deploy tự động
* Có **migration strategy chuẩn production**

---

# 🧠 Kiến thức cốt lõi tuần này

Bạn sẽ hiểu:

| Topic               | Tại sao quan trọng                      |
| ------------------- | --------------------------------------- |
| Load testing        | production system luôn bị spike traffic |
| Database bottleneck | DB thường là điểm nghẽn                 |
| Concurrency         | nhiều request cùng lúc                  |
| CI/CD               | deploy không manual                     |
| Database migration  | schema thay đổi an toàn                 |

---

# 📊 WEEK STRUCTURE

| Day   | Chủ đề                            |
| ----- | --------------------------------- |
| Day 1 | Performance & Load Testing Theory |
| Day 2 | API Load Simulation               |
| Day 3 | Database Stress Test              |
| Day 4 | CI/CD Pipeline                    |
| Day 5 | Migration Strategy                |
| Day 6 | Load Test Analysis                |
| Day 7 | Final Test + Sprint Retrospective |

---

# 📆 DAILY PLAN (3h/day)

---

# 🟢 Day 1 – Load Testing Fundamentals

## 🎯 Mục tiêu

Hiểu:

* load testing là gì
* latency vs throughput
* bottleneck ở đâu

---

## 🧠 Theory (60 phút)

Học các khái niệm:

### Latency

```
Request → Response time
```

Ví dụ:

```
GET /predict
200ms
```

---

### Throughput

```
Requests / second
```

Ví dụ:

```
500 req/s
```

---

### Concurrency

Bao nhiêu request cùng lúc.

```
10 users
100 users
1000 users
```

---

### Bottleneck phổ biến

| Layer   | Vấn đề       |
| ------- | ------------ |
| CPU     | ML inference |
| DB      | slow query   |
| Network | proxy        |
| Disk    | logging      |

---

## 📚 Học ở đâu

Video:

"Load Testing Explained"

[https://www.youtube.com/watch?v=3Y8bIuHf4k4](https://www.youtube.com/watch?v=3Y8bIuHf4k4)

---

## 🤖 Dùng LLM học nhanh

Prompt:

```
Explain load testing vs stress testing vs spike testing.
Give examples for API systems.
```

---

## 🧪 Mini Practice

Test API bằng `curl` loop

```
for i in {1..100}
do
curl http://localhost:8000/health
done
```

Quan sát log.

---

# 🟢 Day 2 – API Load Simulation

## 🎯 Mục tiêu

Simulate traffic vào FastAPI.

---

## 🧠 Tool học

### Locust

Tool load test Python.

---

## 📦 Install

```
pip install locust
```

---

## 🧱 Tạo test script

```
locustfile.py
```

```python
from locust import HttpUser, task

class APIUser(HttpUser):

    @task
    def predict(self):
        self.client.get("/health")
```

---

## 🚀 Run

```
locust
```

Open:

```
http://localhost:8089
```

---

## Test scenarios

| Users | Spawn rate |
| ----- | ---------- |
| 10    | 2/s        |
| 50    | 5/s        |
| 100   | 10/s       |

---

## Deliverable

```
docs/load_test_day2.md
```

Ghi lại:

```
latency
fail rate
req/sec
```

---

# 🟢 Day 3 – Database Stress Test

Tuần trước bạn đã có:

* PostgreSQL
* event table

Giờ test insert.

---

## 🎯 Mục tiêu

Simulate:

```
1k insert
10k insert
concurrent insert
```

---

## 🧪 Python script

```
scripts/load_insert.py
```

```python
import psycopg2
import uuid

conn = psycopg2.connect(
    dbname="ads",
    user="postgres",
    password="password",
    host="localhost"
)

cursor = conn.cursor()

for i in range(1000):

    cursor.execute("""
    INSERT INTO event
    (id, user_id, ad_id, event_type)
    VALUES (%s,%s,%s,%s)
    """,(
        str(uuid.uuid4()),
        1,
        1,
        "impression"
    ))

conn.commit()
```

---

## Test scenarios

| Test   | Rows |
| ------ | ---- |
| small  | 1k   |
| medium | 10k  |
| large  | 100k |

---

## Measure

```
time
CPU
RAM
```

---

## Deliverable

```
docs/db_load_test.md
```

---

# 🟢 Day 4 – CI/CD Pipeline

## 🎯 Mục tiêu

Tự động:

```
push → build → deploy
```

---

## 🧠 CI/CD flow

```
Git push
↓
GitHub Actions
↓
Docker build
↓
Push image
↓
SSH deploy
```

---

## 📂 Tạo file

```
.github/workflows/deploy.yml
```

---

## Example

```yaml
name: Deploy

on:
  push:
    branches: [main]

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v3

      - name: Build Docker
        run: docker build -t api .

      - name: Deploy
        run: |
          ssh user@server "
          docker pull api
          docker restart api
          "
```

---

## Deliverable

Repo có CI chạy.

---

# 🟢 Day 5 – Database Migration Strategy

## 🎯 Mục tiêu

Hiểu:

```
schema evolution
```

---

## Vấn đề thực tế

Production DB không thể:

```
DROP TABLE
```

---

## Best practice

```
migration/
```

```
001_create_tables.sql
002_add_index.sql
003_add_column.sql
```

---

## Rollback

```
down.sql
```

---

## Migration example

```
ALTER TABLE event
ADD COLUMN created_at TIMESTAMP;
```

---

## Deliverable

```
docs/migration_strategy.md
```

---

# 🟢 Day 6 – Load Test Analysis

Bạn phải đọc dữ liệu load test.

---

## Phân tích

| Metric      | Ý nghĩa     |
| ----------- | ----------- |
| P95 latency | 95% request |
| error rate  | fail        |
| throughput  | capacity    |

---

## Ví dụ report

```
Users: 100
Avg latency: 120ms
P95 latency: 300ms
Fail rate: 0%
```

---

## Deliverable

```
docs/performance_report.md
```

---

# 🟢 Day 7 – Week 4 Final Test

## 🧪 Level 1 – Basic

1️⃣ Load testing là gì
2️⃣ latency vs throughput
3️⃣ CI/CD là gì

---

## 🧪 Level 2 – Intermediate

4️⃣ Vì sao DB là bottleneck phổ biến?
5️⃣ Khi nào cần index thêm?
6️⃣ Migration rollback là gì?

---

## 🧪 Level 3 – Advanced

7️⃣ System 1M event/day cần test load thế nào?
8️⃣ Nếu API latency tăng đột ngột thì debug sao?
9️⃣ CI/CD fail deploy xử lý thế nào?

---

# 📊 Week 4 KPI

Bạn hoàn thành khi:

✔ Load test API
✔ DB insert benchmark
✔ CI/CD deploy chạy
✔ Migration strategy defined
✔ Performance report viết xong

---

# 📊 Sprint 2 Retrospective

Viết file:

```
docs/sprint2_retrospective.md
```

Format:

```
What worked
What failed
Technical debt
Next sprint plan
```

---

# 📦 Sau Week 4 bạn đã có gì

Bạn đã build được **mini production system**:

```
Internet
   ↓
Nginx
   ↓
FastAPI
   ↓
PostgreSQL
```

và có:

```
CI/CD
Load testing
Backup
Migration
```

Đây đã là **90% nền tảng backend production**.

---

💡 Nếu bạn muốn, mình có thể làm thêm một thứ **rất quan trọng cho roadmap này**:

### 📊 **"Month 1 Architecture Diagram (Production-grade)"**

một sơ đồ kiến trúc hoàn chỉnh cho:

```
VPS
Docker
Nginx
FastAPI
PostgreSQL
CI/CD
Logs
Backup
```

để từ **Month 2 → Month 9 bạn scale dần hệ thống này** giống hệ thống thật.
