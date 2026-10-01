# 🛡️ Aetheria Admin Panel Specification (Comprehensive)

* **Target Ecosystem:** `Aetheria-Website` ↔ `Aetheria-Social-Backend`
* **Target Users:** Platform Admins, System Engineers, Community Moderators, Content Reviewers
* **Authentication:** JWT Role-Based Access Control (`System`, `Admin`, `Moderator`, `Reviewer`)

---

## 🛠️ Core Administrative Modules

### 1. User & Identity Management (`/admin/users`)
* **Search & Deep Lookup:** Filter users by Username, User ID, Email, IP Address, or Linked OAuth/Hardware Hash.
* **Account Status Controls:**
  * **Role Mutation:** Assign/revoke roles (`User`, `Reviewer`, `Moderator`, `Admin`).
  * **Session Management:** Inspect active login locations/devices and trigger **Global Session Invalidation** (force logout).
  * **Account Lifecycle:** Soft-delete, hard-delete (GDPR compliance), or freeze accounts pending investigation.
* **Moderation Actions & Safety Enforcement:**
  * **Escalated Actions:** Mute (Voice/Text), Kick from Instance, Temporary Ban (Time-boxed), Permanent IP/Hardware Ban.
  * **Appeals Workflow:** Review user-submitted ban/mute appeal tickets with internal staff notes and resolution tracking.
  * **Trust & Safety Score:** View automated risk ratings based on spam flags, block counts, and report velocity.

---

### 2. Live Instance & Server Orchestration (`/admin/instances`)
* **Global Instance Directory:** Real-time table of all active `Aetheria-Unity` server hosts.
  * **Filters:** Map/World, Region, Privacy Level (Public, Friends, Invite-Only), Player Count, Server Build Version.
* **Instance Detail View:**
  * Live player roster with ping, platform type (VR/Desktop), and individual kick/mute controls.
  * Server resource telemetry (CPU, RAM usage, network tick rate, packet loss).
* **Remote Host Operations:**
  * **Host Actions:** Graceful shutdown (with in-game broadcast warning), Force Terminate, or Server Eviction/Migration.
  * **Broadcast Messaging:** Send global or per-instance announcements (e.g., "Server restarting in 5 minutes").

---

### 3. Asset Pipeline & Moderation (`/admin/assets`)
* **Asset Queue (`/admin/assets/queue`):** Review pending `.bee` packages submitted via `Aetheria-SDK` or user portal.
* **Inspection Tools:**
  * 3D Web Viewer / Thumbnail Inspector for avatar and world previews.
  * Automated Virus / Malicious Script scan results (evaluating custom shaders and executable bundles).
  * File size, polygon count, texture size, and optimization check flags.
* **Action Matrix:**
  * **Approve / Feature:** Publish to the local BeeBa catalog.
  * **Flag / Quarantined:** Hide from public directory while awaiting creator updates.
  * **Reject / DMCA Takedown:** Purge `.bee` assets from MinIO and mark records as revoked.

---

### 4. Community Reports & Audit Logs (`/admin/reports`)
* **User Report Management:**
  * Queue for in-game user reports (e.g., harassment, abusive avatars, world exploits).
  * Attached evidence context: Voice clip snippets (if recorded), chat logs, player proximity snapshots, and screenshot attachments.
* **Immutable System Audit Logs (`/admin/audit-logs`):**
  * Searchable event log tracking *who* executed *what* administrative action and *when*.
  * Prevents admin abuse by logging role changes, bans, instance terminations, and manual database edits.

---

### 5. System Health & Infrastructure (`/admin/system`)
* **Service Telemetry:** Real-time health status dashboard for:
  * `Aetheria-Social-Backend` API nodes
  * PostgreSQL (connection pools, slow query alerts)
  * Redis (pub/sub latency, presence cache state)
  * MinIO (storage quota, read/write bandwidth)
  * BeeBa Catalog Service
* **Feature Flags & Configuration:**
  * Toggle system-wide features without code redeployment (e.g., Disable New User Registrations, Toggle Asset Upload Queue, Force Maintenance Mode).

---

## 🔐 Security & Access Control Matrix

| Action / Module | Reviewer | Moderator | Admin | System / Owner |
| :--- | :---: | :---: | :---: | :---: |
| Review Asset Queue & Approve `.bee` | ✅ | ✅ | ✅ | ✅ |
| Kick / Mute / Temp-Ban Users | ❌ | ✅ | ✅ | ✅ |
| Permanent Ban / IP Ban | ❌ | ❌ | ✅ | ✅ |
| Kill Active Room Instances | ❌ | ✅ | ✅ | ✅ |
| Role Assignment & System Flags | ❌ | ❌ | ❌ | ✅ |
