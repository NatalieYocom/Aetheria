# 🎭 Aetheria Avatar Pipeline & Visibility Specification

* **Repository Scope:** `Aetheria-Website` ↔ `Aetheria-Social-Backend` ↔ `Aetheria-Unity`
* **Storage Engine:** MinIO (Local S3-Compatible Object Store)
* **Catalog Service:** Integrated BeeBa Protocol

---

## 🎯 Purpose
Define how avatars are uploaded, reviewed, and rendered across the Aetheria ecosystem. The pipeline ensures creators can immediately test avatars with their inner circle while enforcing platform safety before public indexing.

---

## 🔄 Lifecycle & Approval Flow

When an avatar is compiled via `Aetheria-SDK` and uploaded, it passes through three distinct validation phases:

```text
┌──────────────────┐      Upload      ┌──────────────────┐
│  Aetheria-SDK /  ├─────────────────►│ Storage (MinIO)  │
│  Aetheria-Web    │                  │  & Postgres Rec  │
└──────────────────┘                  └────────┬─────────┘
                                               │
                                               ▼
                                   approval_status = 'pending'
                                               │
                   ┌───────────────────────────┴───────────────────────────┐
                   │                                                       │
                   ▼                                                       ▼
        Requester = Creator / Friend                            Requester = Public
                   │                                                       │
         [ ALLOW VISIBILITY ]                                     [ DENY VISIBILITY ]
                   │                                                       │
                   └───────────────────────────┬───────────────────────────┘
                                               │
                                     Admin / Mod Review
                                               │
                       ┌───────────────────────┴───────────────────────┐
                       │                                               │
                       ▼                                               ▼
             approval_status = 'approved'                    approval_status = 'rejected'
                       │                                               │
       Evaluates visibility Column:                           Hidden from All Users
       • Public ──► Indexed in Catalog                        (Quarantined in MinIO)
       • Unlisted ► Direct Link / Token Only
       • Private ──► Creator Only
