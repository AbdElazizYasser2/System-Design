# 🏗️ System Design Summary

A clean, practical reference for core System Design concepts — covering both theory and real-world examples.

---

## 📚 Table of Contents

- [Load Balancing](#load-balancing)
- [Microservices](#microservices)
- [Monolithic Architecture](#monolithic-architecture)
- [Indexing](#indexing)

---

## ⚖️ Load Balancing

**What is it?**  
Distributes incoming traffic across multiple servers to avoid overloading a single one.

**Types:**
- **Round Robin** — requests go to each server in order
- **Least Connections** — sends to the server with fewest active connections
- **IP Hashing** — same client always hits the same server

**Example:**
```
Client → Load Balancer → [Server 1 | Server 2 | Server 3]
```

**When to use it:**  
High-traffic applications where a single server would become a bottleneck.

---

## 🧩 Microservices

**What is it?**  
Breaking an application into small, independent services that each handle one responsibility.

**Key traits:**
- Each service has its own database
- Services communicate via APIs (REST / gRPC / Message Queues)
- Independent deployment and scaling

**Example:**
```
[User Service] → [Order Service] → [Payment Service]
      ↓                ↓                  ↓
  [Users DB]      [Orders DB]        [Payments DB]
```

**Pros:**
- Scale each service independently
- Teams can work in parallel
- Failure in one service doesn't crash the whole app

**Cons:**
- More complex to manage and monitor
- Network overhead between services

---

## 🏛️ Monolithic Architecture

**What is it?**  
The entire application is built and deployed as a single unit.

**Example:**
```
[ One Big App ]
  - Auth
  - Orders
  - Payments
  - Notifications
       ↓
  [Single DB]
```

**Pros:**
- Simple to develop and deploy (especially early on)
- Easier to debug and test
- No network overhead

**Cons:**
- Hard to scale specific parts
- One bug can bring the whole system down
- Becomes messy as the codebase grows

**Monolith vs Microservices — Quick Comparison:**

| | Monolith | Microservices |
|---|---|---|
| Deployment | Single unit | Independent services |
| Scaling | Scale everything | Scale per service |
| Complexity | Low (at start) | High |
| Best for | Small teams / MVPs | Large scale systems |

---

## 🗂️ Indexing

**What is it?**  
A data structure that speeds up read queries on a database by avoiding full table scans.

**How it works:**
```
Without index → scan every row   → slow 🐢
With index    → jump to the row  → fast ⚡
```

**Types:**
- **Primary Index** — on the primary key (auto-created)
- **Secondary Index** — on any other column (e.g. email, username)
- **Composite Index** — on multiple columns together

**Example (SQL):**
```sql
-- Without index: full scan on 10M rows
SELECT * FROM users WHERE email = 'test@example.com';

-- Add index
CREATE INDEX idx_email ON users(email);

-- Now the query is instant ⚡
```

**Trade-offs:**
- ✅ Faster reads
- ❌ Slower writes (index must be updated on every insert/update)
- ❌ Extra storage

**Rule of thumb:** Index columns you frequently filter or sort by — don't over-index.

---
---

> ⭐ If this helped you, consider giving the repo a star!
