# Enterprise AI Operations & Collaboration Command Center

> Production-Grade Enterprise AI Platform connecting organizational data, departmental workflows, operational search, intelligent workflow orchestration, and generative decision support.

---

## 1. Architectural Highlights

- **Frontend**: React 18, Vite, TypeScript, Tailwind CSS, TanStack Query, React Router v6, Lucide React icons.
- **Backend**: Node.js, Express, TypeScript, REST API Architecture, Helmet, Cookie-Parser, Rate Limiting.
- **Database Engine**: Dual-mode PostgreSQL support:
  - Connects to external PostgreSQL / Replit Postgres / AWS RDS / Neon / Supabase via `DATABASE_URL`.
  - Embedded, zero-configuration PostgreSQL engine powered by `@electric-sql/pglite` with persistent disk storage in `./data/postgres`.
  - Full relational integrity, UUID primary keys, foreign keys, triggers, constraints, and indexes.
- **AI Engine**:
  - Official Google Gen AI SDK (`@google/genai`) running strictly **server-side**.
  - All AI outputs validated against **strict Zod schemas** before returning to the client.
  - Context grounding with prompt-injection filtering.
  - Zero-downtime deterministic intelligence fallback if `GEMINI_API_KEY` is not yet configured.
  - In-app AI & security settings to configure or update API keys and Gemini models.
- **Multi-Tenant Data Isolation**:
  - Strict organization-level data isolation (`organization_id UUID NOT NULL` on every entity).
  - Server-side session verification; client-supplied IDs are never trusted.
- **Role-Based Access Control (RBAC)**:
  - `employee`
  - `manager`
  - `department_admin`
  - `organization_admin`

---

## 2. Default Seed Personas (1-Click Login)

The database automatically seeds realistic departments, strategic projects, tasks, governance policies, meeting transcripts, and AI insights.

| Name | Email | Role | Department | Default Password |
|---|---|---|---|---|
| **Alex Morgan** | `alex.morgan@acme.com` | `organization_admin` | Administration | `Password123!` |
| **Sarah Chen** | `sarah.chen@acme.com` | `department_admin` | Engineering | `Password123!` |
| **David Miller** | `david.miller@acme.com` | `manager` | Product | `Password123!` |
| **Emily Watson** | `emily.watson@acme.com` | `employee` | Engineering | `Password123!` |
| **Marcus Vance** | `marcus.vance@acme.com` | `employee` | Marketing | `Password123!` |

---

## 3. Getting Started

### Prerequisites
- Node.js 18+ (tested on Node v24)
- npm 9+

### Environment Setup
Copy the example environment configuration:
```bash
cp .env.example .env
```

Contents of `.env`:
```env
NODE_ENV=development
PORT=5000
DATABASE_URL=
GEMINI_API_KEY=
SESSION_SECRET=enterprise_super_secret_session_key_2026_jwt_token_sign_key
CORS_ORIGIN=http://localhost:5173
```

*(Note: If `GEMINI_API_KEY` is left blank, the application automatically activates its deterministic intelligence engine while allowing in-app API key configuration in Settings).*

### Running Locally

```bash
# 1. Install root & client dependencies
npm install
npm --prefix client install

# 2. Run database migrations & seed dataset
npm run db:seed

# 3. Start development server (both server on port 5000 and client on 5173)
npm run dev

# 4. Or build and run production bundle
npm run build
npm start
```

Access the application in your browser at:
- **Development**: [http://localhost:5173](http://localhost:5173)
- **Production Server**: [http://localhost:5000](http://localhost:5000)

---

## 4. Key Functional Capabilities

1. **Role-Aware Dashboard**: Dynamic KPI calculations, active strategic projects, assigned workload, upcoming deadlines, AI risk radar, and recent audit activity.
2. **AI Enterprise Assistant**: Grounded Q&A against live tasks, projects, SOPs, and meetings with cited source references, evidence points, and follow-up inquiry suggestions.
3. **Enterprise Knowledge Search**: Natural-language search across documents, policies, tasks, projects, and meetings with contextual snippets and relevance scoring.
4. **Intelligent Task Management**: Task creation, assignments, status transitions (`todo`, `in_progress`, `blocked`, `completed`, `cancelled`), priority levels (`low`, `medium`, `high`, `critical`), dependencies, and comment threads.
5. **AI Task Generator**: Converts unstructured text or directives into structured tasks with human confirmation before persisting to PostgreSQL.
6. **Project Management**: Cross-departmental initiatives, progress tracking, deliverable velocity, and contributor rosters.
7. **Department Management**: Workspaces for Engineering, Product, Marketing, Sales, Finance, HR, Operations, Support, Legal & Compliance, and Administration.
8. **Document Management & AI Summarization**: Centralized SOPs, governance policies, and technical specifications with on-demand AI executive summarization.
9. **Meeting Intelligence**: Meeting transcript analysis with automated extraction of decisions, owners, deadlines, and 1-click conversion from action items to live database tasks.
10. **Operational Insights & Bottleneck Detection**: Identifies cross-functional blockers, overdue deliverables, and workload saturation with recommended remediations.
11. **AI Executive Reporting**: Automated synthesis of high-level management reports, achievements, and priorities across customizable horizons (7 days, 30 days, quarterly).
12. **Audit & Activity Logs**: Immutable logging of system events, authentication, role changes, and data mutations.
13. **Security & AI Configuration**: Manage API keys, Gemini models, and organization membership.

---

## 5. Verification Suite

Run the automated end-to-end verification script:
```powershell
powershell -ExecutionPolicy Bypass -File test_suite.ps1
```
All 13 integration tests validate API health, authentication, RBAC, AI chat, task generation, search, summarization, meeting analysis, reporting, and audit trails.
