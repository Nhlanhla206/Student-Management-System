[README.md](https://github.com/user-attachments/files/30204319/README.md)
# Student-Management-System
**Student Management System:** A centralized platform that enables students, lecturers, faculty administrators, and administrative staff to manage academic records, course registrations, grades, attendance, fees, and student performance, improving communication, efficiency, and decision-making across the institution.
# NWU Student Data Management System (SDMS)

**Enterprise-Grade Student Information System for North-West University**

A comprehensive, feature-rich student management platform built with pure JavaScript (frontend) and PostgreSQL (backend), designed to manage the complete student lifecycle — from enrollment and academics to finance, bursaries, attendance tracking, and system health monitoring.

---

## 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Architecture](#-architecture)
3. [Technology Stack](#-technology-stack)
4. [Key Features](#-key-features)
5. [System Modules](#-system-modules)
6. [Database Schema](#-database-schema)
7. [User Roles & Access Control](#-user-roles--access-control)
8. [Quick Start](#-quick-start)
9. [Deployment](#-deployment)
10. [API & Functions](#-api--functions)
11. [Security & Compliance](#-security--compliance)
12. [BI & Analytics](#-bi--analytics)
13. [Project Structure](#-project-structure)
14. [File Reference](#-file-reference)
15. [Future Roadmap](#-future-roadmap)

---

## 🎯 Project Overview

The **NWU Student Data Management System** is a browser-based administrative dashboard that provides university staff with real-time visibility into student data across five faculties. It simulates an enterprise SIS (Student Information System) with role-based dashboards, intelligent analytics, automated bursary evaluation, attendance tracking via location scans, and comprehensive financial management.

**Purpose:** This project serves as both a **functional prototype** and an **educational showcase** of database design (3NF/5NF normalization), full-stack JavaScript development, and enterprise-grade PostgreSQL schema engineering.

### Core Capabilities

| Capability | Description |
|---|---|
| **Student Lifecycle** | From enrollment through graduation, including risk tracking |
| **Financial Management** | Fee structures, payment plans, receipts, blocking/unblocking |
| **Intelligent Bursaries** | Auto-eligibility engine with 7 bursary types and override workflows |
| **Attendance Ecosystem** | Location scans, manual attendance, discrepancy detection, verification |
| **Role-Based Access** | 5 distinct roles with faculty-scoped data visibility |
| **Real-Time Simulation** | Live-updating student metrics, scans, and notifications |
| **System Monitoring** | Database, API, storage health; CI/CD pipeline; performance metrics |
| **BI Analytics** | Star-schema data warehouse with materialized views and fact tables |

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                        BROWSER (Frontend)                          │
│                                                                     │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌───────────────────┐  │
│  │index.html│  │style.css │  │script.js │  │   database.js     │  │
│  │  (UI)    │  │  (Theme) │  │  (Logic) │  │  (Mock Data Gen)  │  │
│  └──────────┘  └──────────┘  └──────────┘  └───────────────────┘  │
│         │              │              │               │            │
│         └──────────────┴──────────────┴───────────────┘            │
│                            │                                       │
│                    ┌───────┴───────┐                               │
│                    │  Chart.js CDN │                               │
│                    │  Supabase SDK │                               │
│                    └───────────────┘                               │
└─────────────────────────┬──────────────────────────────────────────┘
                          │
              ┌───────────┴────────────┐
              │   Options Layer        │
              │  ┌────────────────┐    │
              │  │  Client-Side   │    │
              │  │  Mock Database │    │
              │  └────────────────┘    │
              │  ┌────────────────┐    │
              │  │  Supabase      │    │
              │  │  PostgreSQL    │    │
              │  └────────────────┘    │
              └────────────────────────┘
                          │
              ┌───────────┴───────────────────────────────┐
              │          PostgreSQL Database               │
              │  ┌─────────┐ ┌────────┐ ┌──────────┐    │
              │  │ 3NF/5NF │ │  Star  │ │Functions │    │
              │  │ Schema  │ │ Schema │ │& Triggers│    │
              │  └─────────┘ └────────┘ └──────────┘    │
              └─────────────────────────────────────────┘
```

### Two Deployment Modes

1. **Standalone (Client-Side Only):** Open `index.html` in a browser. All 500 students, lecturers, bursary applications, and 2000+ location scans are generated in-memory by `database.js`. No server or database required.

2. **Supabase-Powered:** Deploy the SQL migration to Supabase PostgreSQL for persistence, real-time sync, and production-scale capabilities.

---

## 💻 Technology Stack

### Frontend
| Technology | Purpose |
|---|---|
| **HTML5** | Semantic structure with ARIA accessibility |
| **CSS3** | Custom properties, dark/light themes, responsive design |
| **Vanilla JavaScript (ES6+)** | All application logic, no frameworks |
| **Chart.js 4.4** | Interactive charts (line, bar, doughnut) |
| **Font Awesome 6** | Icons throughout the UI |
| **Google Fonts (Inter)** | Typography |

### Database
| Technology | Purpose |
|---|---|
| **PostgreSQL 16+** | Primary database |
| **Supabase** | Hosted Postgres + Auth (optional) |
| **pgcrypto** | Password hashing |
| **uuid-ossp** | UUID generation |
| **ltree** | Hierarchy queries |
| **btree_gin** | Composite indexing |
| **pg_stat_statements** | Query monitoring |

### Tooling
| Tool | Purpose |
|---|---|
| **Node.js** | Debug scripts, seed data execution |
| **pg (node-postgres)** | Database client for debug scripts |
| **pg_cron** | Scheduled maintenance (backup, refresh MVs) |

---

## ✨ Key Features

### 🎛️ Dashboard & Analytics
- **8 KPI Cards**: Active students, on-track rate, at-risk count, outstanding fees, avg attendance, avg mark, blocked accounts, pass rate
- **6 Chart Types**: Attendance trends, faculty distribution, risk distribution, payment trends, module distribution, bursary status
- **Role-Specific Widgets**: Top students (Admin), faculty overview (Faculty Admin), financial/bursary summary (Finance), student alerts & performance table (Lecturer)
- **Real-Time Updates**: Student metrics refresh every 15 seconds with simulated changes

### 👨‍🎓 Student Management
- **500+ Students** across 5 faculties, 20 courses, and 70+ modules
- **Search** by ID, name, or course
- **Sortable Columns**: ID, name, faculty, course, year, attendance, mark, risk level
- **Paginated Views** with adjustable page sizes (10/50/100)
- **Student Detail Modal**: Full profile with financial data, scan history, bursary info
- **Track Location Modal**: Real-time location scanning history with lecturer info
- **Grade Submission**: Lecturers can submit grades per module

### 👨‍🏫 Lecturer Management
- **12 Core Lecturers** + 150+ generated in bulk seed
- Faculty-scoped visibility
- CRUD operations via modal forms
- Module assignments per lecturer

### 📚 Course & Module Management
- **20 Courses** across 5 faculties
- **70+ Modules** with credit values and faculty mapping
- Course-module curriculum mapping (5NF pure join)
- Module distribution charts by credits and faculty
- Lecturer-module assignment tracking

### 💰 Financial Management
- Complete financial records for all students
- Outstanding fee tracking with blocking at R50,000+
- Payment history and installment plan tracking
- **Receipt Generation**: Computer-generated receipts with bursary funding info
- **Unblock Functionality**: One-click account unblocking
- **Financial Risk Categorization**: Critical (>R50k), High (>R20k), Medium (>R5k), Low
- Faculty-wise outstanding fee breakdown charts
- Collection vs Outstanding trend charts

### 🎓 Intelligent Bursary Management
- **7 Bursary Types**: Academic Merit, Family Discount, Leadership, Support, Arts & Culture, Postgraduate Merit, Special Student Support Fund
- **Auto-Eligibility Engine**: System evaluates students against 17 criteria rules
- **System Auto-Approval**: Students meeting all criteria get instant approval
- **System Auto-Rejection**: Non-qualifying students auto-rejected with reasons
- **Admin Override**: Approve, reject, or suspend with reason audit trail
- **Detail View**: Full eligibility breakdown with pass/fail per criterion
- **Status Tracking**: Approved, Pending, Rejected, Suspended
- **Budget Utilization**: Program budgets with remaining balance tracking
- **Filter Pills**: Filter applications by bursary type
- **Bursary Summary**: Approved, rejected, pending counts with system auto stats

### 📋 Attendance Management
- **Dual Tracking**: Card/biometric scans + manual lecturer attendance
- **Attendance Percentage**: Calculated from scans + manual records
- **Discrepancy Detection**: Flags mismatches between scan and manual records
- **Verification Workflow**: Lecturers can approve or flag discrepancies
- **Module Filtering**: Filter by lecturer's modules
- **Attendance Trends**: Line chart over 12 months

### 📍 Location Scans
- **2,000+ Simulated Scans** across 8 buildings and 30 rooms
- Real-time scan generation every 15 seconds
- Student tracking with building, room, and lecturer context
- Attendance marking status per scan

### ❤️ System Health Monitoring
- **6 Health Cards**: Database, API, Storage, Uptime, Failed Logins, Last Backup
- **CI/CD Pipeline**: 6-stage pipeline with status, duration, and timestamps
- **Performance Metrics**: Active connections, queries/sec, cache hit ratio
- **Server Monitoring**: CPU, RAM, disk usage per server node
- **Storage Alerts**: Warning at 80% capacity

### 📜 Audit & Compliance
- **Comprehensive Audit Logs**: Timestamped, user-attributed actions
- **User Activity Logs**: Login, dashboard views, attendance marking, etc.
- **Severity Levels**: Info, Warning, Important
- **CSV Export**: Export any table to CSV
- **PDF Reports**: Generate formatted reports per section
- **Data Retention Policies**: Automated archiving and deletion schedules
- **Consent Management**: Student data processing consent records
- **Data Access Logs**: All SELECT/INSERT/UPDATE/DELETE operations logged

### 🎨 User Interface
- **Dark/Light Theme**: Toggle with persisted preference
- **Responsive Design**: Desktop, tablet, and mobile layouts
- **Toast Notifications**: Success, error, warning, info messages
- **Modal System**: Detail views, forms, confirmations
- **Search Dropdown**: Global student search from navbar
- **Keyboard Shortcuts**: `Ctrl+T` for timetable, `Ctrl+U` for assignment upload (lecturer)

---

## 📦 System Modules

### Core Domain Tables (50+)

| Domain | Tables |
|---|---|
| **Reference** | `faculty`, `department`, `qualification`, `course`, `module`, `building`, `room` |
| **Join (5NF)** | `faculty_course`, `course_module`, `lecturer_course`, `lecturer_module` |
| **Users** | `app_user`, `role_permission`, `user_session` |
| **People** | `student`, `lecturer` |
| **Academic** | `enrollment`, `module_registration`, `assessment`, `student_mark`, `module_result`, `graduation_checklist` |
| **Attendance** | `scanner_device`, `session_schedule`, `session_instance`, `attendance_scan`, `attendance_discrepancy`, `geofence_zone` |
| **Financial** | `fee_structure`, `student_account`, `transaction`, `payment_plan` |
| **Bursary** | `bursary_program`, `bursary_criterion`, `bursary_application`, `bursary_document`, `bursary_disbursement`, `bursary_override_action`, `nsfas_record` |
| **Student Life** | `residence`, `residence_room`, `residence_allocation`, `library_access_log`, `library_loan`, `wellness_visit`, `disciplinary_record` |
| **Employability** | `employability_profile`, `internship_placement`, `career_event_attendance` |
| **Risk** | `risk_factor`, `intervention` |
| **Notifications** | `notification`, `alert` |
| **System** | `service_health`, `db_performance_log`, `api_performance_log`, `server_health_log`, `security_event` |
| **ETL** | `etl_pipeline`, `pipeline_run`, `stage_student_import`, `stage_financial_import`, `schema_version`, `data_retention_policy` |
| **BI (Star Schema)** | `dim_date`, `dim_student`, `dim_faculty`, `dim_bursary_program`, `fact_academic_performance`, `fact_financial`, `fact_attendance`, `fact_bursary` |
| **Governance** | `consent_record`, `data_access_log` |

---

## 🗄 Database Schema

The project includes **three schema variants** designed for different environments:

### 1. 5NF Schema (`nwu_schema_5nf.sql`)
- **SQL Server compatible** (uses `IDENTITY`, `DATETIME2`, `BIT`)
- Fifth Normal Form (5NF) — all join tables are pure relationships
- Complete separation of multivalued dependencies
- Includes: `FacultyCourse`, `CourseModule`, `LecturerCourse`, `LecturerModule`, `BursaryCriterion`, `BursaryCriteriaMet`, `BursaryEligibilityOverride`, `BursaryOverrideAction`
- 25+ tables with seed data

### 2. Production Schema (`nwu_production_schema.sql`)
- **PostgreSQL 16+** with 24 parts
- 50+ tables with full normalization (3NF/5NF)
- Custom domains: `email_address`, `south_african_id`, `currency_amount`, `percentage`, `score_100`, `year_level`
- 12 **stored procedures** including:
  - `fn_authenticate_user()` — Secure login with bcrypt
  - `fn_evaluate_bursary_eligibility()` — Dynamic criteria evaluation engine
  - `fn_get_student_profile()` — Full student profile
  - `fn_faculty_dashboard()` — Faculty-level KPI aggregation
  - `fn_generate_graduation_list()` — Ceremony-ready graduation candidates
  - `fn_archive_old_records()` — Data retention automation
  - `fn_create_student_account()` — Auto-account creation
  - `fn_update_account_balance()` — Real-time balance updates
  - `fn_update_graduation_status()` — Automatic status recalculation
  - `fn_refresh_student_metrics()` — Periodic metric refresh
  - `fn_lock_account_on_failures()` — Security lockout after 5 failures
  - `fn_log_security_event()` — SIEM integration
- 7 **views**: `v_active_students`, `v_student_bursary_summary`, `v_financial_risk`, `v_attendance_anomalies`, `v_system_health_overview`, `v_bursary_budget_utilization`
- 2 **materialized views**: `mv_daily_attendance_summary`, `mv_student_risk_snapshot`
- **Partitioning**: `attendance_scan`, `transaction`, `api_performance_log` partitioned by time
- **Row-Level Security (RLS)**: Faculty-scoped and lecturer-scoped policies
- **Data Retention**: Policy-driven archiving strategy

### 3. Supabase Migration (`nwu_supabase_migration.sql`)
- Supabase-compatible (avoids `CREATE ROLE`, uses `TEXT` instead of `VARCHAR`)
- Includes authentication function using `pgcrypto`
- All tables, triggers, views, and materialized views
- Production-ready for Supabase hosting

---

## 👥 User Roles & Access Control

The system implements **Role-Based Access Control (RBAC)** with five distinct roles:

| Role | Email | Password | Access Scope |
|---|---|---|---|
| **Super Admin** | `admin@nwu.ac.za` | `admin123` | Full system — all sections, all faculties |
| **Faculty Admin** | `engadmin@nwu.ac.za` (Engineering) | `faculty` | Faculty-scoped: students, lecturers, courses, attendance, scans |
| | `sciadmin@nwu.ac.za` (Science) | `faculty` | Same scope, different faculty |
| | `busadmin@nwu.ac.za` (Business) | `faculty` | Same scope, different faculty |
| | `eduadmin@nwu.ac.za` (Health) | `faculty` | Same scope, different faculty |
| | `lawadmin@nwu.ac.za` (Arts) | `faculty` | Same scope, different faculty |
| **Lecturer** | `lec001@nwu.ac.za` (Dr. Thandi Mokoena) | `lecture` | Module-scoped: dashboard, students, modules, attendance, scans |
| | `lec002@nwu.ac.za` through `lec005@nwu.ac.za` | `lecture` | Same scope, different modules |
| **Finance Officer** | `finance@nwu.ac.za` | `finance` | Dashboard, finance, bursary sections |

### Role-Based Section Visibility

| Section | Admin | Faculty Admin | Lecturer | Finance |
|---|---|---|---|---|
| Dashboard | ✅ | ✅ | ✅ | ✅ |
| Students | ✅ | ✅ | ✅ | ❌ |
| Lecturers | ✅ | ✅ | ❌ | ❌ |
| Courses | ✅ | ✅ | ❌ | ❌ |
| Modules | ✅ | ❌ | ✅ | ❌ |
| Finance | ✅ | ❌ | ❌ | ✅ |
| Bursaries | ✅ | ❌ | ❌ | ✅ |
| Attendance | ✅ | ✅ | ✅ | ❌ |
| Scans | ✅ | ✅ | ✅ | ❌ |
| System Health | ✅ | ❌ | ❌ | ❌ |
| Audit Logs | ✅ | ❌ | ❌ | ❌ |

---

## 🚀 Quick Start

### Option 1: Standalone (No Server Required)

1. **Clone or download** the project files
2. **Open `index.html`** in any modern browser (Chrome, Firefox, Edge recommended)
3. **Log in** using one of the credentials above (default: `admin@nwu.ac.za` / `admin123`)
4. The system generates **500 students**, **12 lecturers**, **2000+ location scans**, and **120+ bursary applications** in-memory
5. Click the **Quick Access chips** on the login screen to auto-fill credentials

### Option 2: Supabase PostgreSQL

1. **Create a Supabase project** at [supabase.com](https://supabase.com)
2. **Run the migration script** `nwu_supabase_migration.sql` in the Supabase SQL Editor
3. **Seed the database** by running:
   - `nwu_seed_data.sql` (reference data)
   - `nwu_bulk_seed.sql` (generated data — 500+ students, 150+ lecturers, etc.)
4. **Update `database.js`** connection settings:
   ```javascript
   // Enable Supabase mode
   window.useSupabase = () => true;
   
   // Configure your Supabase URL and anon key
   const supabaseUrl = 'https://your-project.supabase.co';
   const supabaseAnonKey = 'your-anon-key';
   ```
5. **Open `index.html`** — the app will authenticate against and read from your Supabase database

### Option 3: Local PostgreSQL

1. **Install PostgreSQL 16+** on your machine
2. **Create the database**:
   ```sql
   CREATE DATABASE nwu_sdms ENCODING 'UTF8' LC_COLLATE 'en_ZA.UTF-8';
   ```
3. **Run the production schema**:
   ```bash
   psql -U postgres -d nwu_sdms -f nwu_production_schema.sql
   ```
4. **Run seed data**:
   ```bash
   psql -U postgres -d nwu_sdms -f nwu_seed_data.sql
   psql -U postgres -d nwu_sdms -f nwu_bulk_seed.sql
   ```
5. **Configure the debug scripts** or build an API layer to connect the frontend

---

## 🚢 Deployment

### Database Deployment Checklist

```sql
-- 1. Create database
CREATE DATABASE nwu_sdms;

-- 2. Run schema
\i nwu_supabase_migration.sql

-- 3. Seed reference data
\i nwu_seed_data.sql

-- 4. Generate bulk data (5-10 minutes)
\i nwu_bulk_seed.sql

-- 5. Set up cron jobs
SELECT cron.schedule('archive-job', '0 3 * * 0', 
    'SELECT fn_archive_old_records();');
SELECT cron.schedule('refresh-mviews', '0 2 * * *', 
    'REFRESH MATERIALIZED VIEW mv_daily_attendance_summary;');
SELECT cron.schedule('refresh-risk', '0 1 * * *', 
    'REFRESH MATERIALIZED VIEW mv_student_risk_snapshot;');

-- 6. Create read-only BI role
CREATE ROLE bi_reader LOGIN PASSWORD 'bi_password';
GRANT SELECT ON ALL TABLES IN SCHEMA public TO bi_reader;
```

### Scaling Considerations

- **Connection Pooling**: Use PgBouncer for connection management
- **Read Replicas**: Direct BI queries to replicas
- **Partitioning**: Monthly partitions for `attendance_scan` and `transaction`
- **WAL Archiving**: Enable for point-in-time recovery
- **Streaming Replication**: For high availability

---

## ⚙️ API & Functions

### Key Stored Procedures

```sql
-- Authenticate user with bcrypt
SELECT * FROM fn_authenticate_user('admin@nwu.ac.za', 'admin123');

-- Get full student profile
SELECT * FROM fn_get_student_profile('41234567');

-- Evaluate bursary eligibility
SELECT * FROM fn_evaluate_bursary_eligibility('41234567', 'merit');

-- Faculty dashboard KPIs
SELECT * FROM fn_faculty_dashboard('FAC001');

-- Generate graduation list
SELECT * FROM fn_generate_graduation_list(2025, '2025-12-15');
```

### Views for Reporting

```sql
-- Active students (matches frontend logic)
SELECT * FROM v_active_students;

-- Financial risk assessment
SELECT * FROM v_financial_risk;

-- Bursary budget utilization
SELECT * FROM v_bursary_budget_utilization;

-- Attendance anomalies
SELECT * FROM v_attendance_anomalies;

-- System health overview
SELECT * FROM v_system_health_overview;
```

---

## 🔒 Security & Compliance

### Implemented Security Measures

| Measure | Implementation |
|---|---|
| **Password Hashing** | `pgcrypto` with bcrypt (`gen_salt('bf')`) |
| **Account Lockout** | Auto-lock after 5 failed login attempts (30 min) |
| **Row-Level Security** | Faculty-scoped and lecturer-scoped policies |
| **Session Management** | UUID sessions with expiry and revocation |
| **MFA Ready** | `mfa_enabled` and `mfa_secret` fields on `app_user` |
| **Security Events** | SIEM-ready logging of all security incidents |
| **Data Access Audit** | Every SELECT/INSERT/UPDATE/DELETE logged |
| **Consent Management** | Student data processing consent tracking |
| **Data Retention** | Policy-driven auto-archiving and deletion |

### RBAC Database Roles

```sql
-- Create roles (if not in Supabase managed)
CREATE ROLE super_admin_role;
CREATE ROLE faculty_admin_role;
CREATE ROLE lecturer_role;
CREATE ROLE finance_role;
CREATE ROLE auditor_role;

-- Grant privileges per role
GRANT ALL ON ALL TABLES TO super_admin_role;
GRANT SELECT, INSERT, UPDATE ON student, faculty, course 
    TO faculty_admin_role;
GRANT SELECT ON student, module, module_result 
    TO lecturer_role;
GRANT SELECT, INSERT, UPDATE ON transaction, student_account 
    TO finance_role;
```

---

## 📊 BI & Analytics

### Star Schema Dimensions

| Dimension | Key Attributes |
|---|---|
| `dim_date` | Full 3-year calendar with academic year, semester, term, holidays |
| `dim_student` | Student demographics, faculty, course, risk, graduation status |
| `dim_faculty` | Faculty info with dean, department count, student count |
| `dim_bursary_program` | Program details, funding source, max amount |

### Star Schema Facts

| Fact Table | Measures | Grain |
|---|---|---|
| `fact_academic_performance` | Final mark, credits, attendance rate, risk score | Per student per module per semester |
| `fact_financial` | Fees, payments, outstanding, bursary amount | Per student per month |
| `fact_attendance` | Session count, present/absent/late counts, anomaly count | Per student per day |
| `fact_bursary` | Amount awarded, eligibility score, days to decision | Per application |

### Materialized Views

- **`mv_daily_attendance_summary`**: Daily attendance rates per module
- **`mv_student_risk_snapshot`**: Current risk profile for all active students

---

## 📁 Project Structure

```
NWU SMS/
│
├── 📄 index.html                  # Main application shell (HTML + inlined modals)
├── 📄 style.css                   # Complete CSS with dark/light themes
├── 📄 script.js                   # All application logic (2500+ lines)
├── 📄 database.js                 # Mock data generator & in-memory database
│
├── 📄 package.json                # Node.js configuration (pg dependency)
├── 📄 package-lock.json           # Dependency lock file
│
├── 📂 SQL/                        # Database schema & seed files
│   ├── 📄 nwu_schema_5nf.sql                # 5NF schema (SQL Server compatible)
│   ├── 📄 nwu_production_schema.sql         # Full PostgreSQL production schema
│   ├── 📄 nwu_supabase_migration.sql        # Supabase migration script
│   ├── 📄 nwu_seed_data.sql                 # Core reference data seed
│   └── 📄 nwu_bulk_seed.sql                 # Bulk data generator (500+ students)
│
├── 📂 Debug Scripts/             # Node.js database connectivity tests
│   ├── 📄 debug_seed.js          # Test bursary program & student account 
├── 📂 Images/
│   └── 📄 Logo.png               # ScholarSphere branding logo
│
└── 📄 README.md                  # This file
```

---

## 📄 File Reference

| File | Lines | Purpose |
|---|---|---|
| `index.html` | ~450 | HTML structure, all modals, CDN links |
| `style.css` | ~900 | Complete theming, responsive layout, component styles |
| `script.js` | ~2500 | All JS logic: auth, routing, data binding, charts, exports, CRUD |
| `database.js` | ~600 | Mock data generation: 500 students, 2000+ scans, bursary engine |
| `nwu_production_schema.sql` | ~1400 | Full 24-part production schema |
| `nwu_supabase_migration.sql` | ~800 | Supabase-compatible schema with auth functions |
| `nwu_schema_5nf.sql` | ~500 | SQL Server 5NF schema |
| `nwu_seed_data.sql` | ~500 | Reference data seed |
| `nwu_bulk_seed.sql` | ~450 | Bulk data generation |

---

## 🗺 Future Roadmap

### Phase 1: Foundation ✅
- [x] Client-side mock database with full CRUD
- [x] 5 roles with RBAC and faculty-scoped views
- [x] Dashboard with 8 KPI cards and 6 chart types
- [x] Student, lecturer, course, and module management
- [x] Financial management with receipts and blocking
- [x] Intelligent bursary auto-eligibility engine
- [x] Dual attendance tracking (scans + manual)
- [x] System health monitoring
- [x] Dark/light theme

### Phase 2: Database Integration 🚧
- [ ] Supabase authentication flow (OAuth, magic link)
- [ ] Real-time subscriptions via Supabase Realtime
- [ ] File upload for bursary documents (Supabase Storage)
- [ ] Server-side pagination and search (PostgreSQL FTS)
- [ ] API gateway (Supabase Edge Functions)

### Phase 3: Enterprise Features 📋
- [ ] Timetable/scheduling with conflict detection
- [ ] Residence allocation and management
- [ ] Library integration with borrowing management
- [ ] Employability/career services tracking
- [ ] Wellness and disciplinary record management
- [ ] Predictive analytics (ML-powered risk prediction)
- [ ] Multi-language support (Afrikaans, Sesotho, Zulu)
- [ ] Mobile app (React Native or Flutter)
- [ ] WhatsApp/SMS notification channel
- [ ] Email reports with automated scheduling

### Phase 4: Scale & Compliance 🏛️
- [ ] POPIA compliance module
- [ ] GDPR-compliant data export/deletion
- [ ] Advanced SIEM integration
- [ ] Load balancing and horizontal scaling
- [ ] Disaster recovery automated testing
- [ ] Penetration testing framework
- [ ] SOC 2 readiness documentation

---

## 📝 License

This project is developed for **NWU INFS614** — Database Design coursework.

---

## 👥 Contributors

- **Senior Database Architect** — Production SQL schema design
- **Frontend Engineer** — Full-stack JavaScript application
- **Data Engineer** — Seed data generation and ETL pipeline

---

*Built with ❤️ for North-West University*

