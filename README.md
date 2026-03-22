<div align="center">

# 🛡️ Teos-Comply-Crawl (TCC)

**AI Compliance Infrastructure — The Legal Firewall for AI Data Pipelines**

[![CI](https://github.com/Elmahrosa/teos-comply-crawl/actions/workflows/ci.yml/badge.svg)](https://github.com/Elmahrosa/teos-comply-crawl/actions/workflows/ci.yml)
[![Security](https://github.com/Elmahrosa/teos-comply-crawl/actions/workflows/security.yml/badge.svg)](https://github.com/Elmahrosa/teos-comply-crawl/actions/workflows/security.yml)
[![Status: SaaS Baseline Ready](https://img.shields.io/badge/Status-SaaS_Baseline_Ready-green?style=flat-square)](#pricing)
[![Deployment](https://img.shields.io/badge/Deployment-Docker-blue?style=flat-square)](deploy/docker-compose.yml)
[![Python](https://img.shields.io/badge/Python-3.12-3776ab?style=flat-square)](https://python.org)
[![License: TESL v2.0](https://img.shields.io/badge/License-TESL_v2.0-red?style=flat-square)](LICENSE)
[![Standards: GovStack](https://img.shields.io/badge/Standards-GovStack_Aligned-blue?style=flat-square)](https://github.com/Elmahrosa/Teos-International-Civic-Blockchain-Constitution/blob/main/docs/compliance/govstack-mapping.yaml)
[![MCP Compatible](https://img.shields.io/badge/MCP-Compatible-purple?style=flat-square)](mcp/server.py)

📧 **[ayman@teosegypt.com](mailto:ayman@teosegypt.com)** · 🌐 **[teosegypt.com](https://teosegypt.com)**

</div>

---

Teos-Comply-Crawl (TCC) is a production-grade API for safer, compliant web ingestion. It acts as a governance layer between AI agents and the open web by enforcing policy, scrubbing detected PII, and logging pipeline decisions before data enters downstream systems.

```text
Old model:  fetch → store → risk         ❌
TCC model:  request → policy → safe fetch → PII scrub → audit log  ✅
```

---

## 🎯 Who This Is For

TCC is designed for:

- **AI developers** building LLM pipelines — RAG systems, agents, ingestion workflows
- **SaaS teams** handling external data ingestion at scale
- **Security-conscious engineering teams** needing SSRF protection and audit trails
- **Compliance and legal teams** requiring structured evidence of data handling
- **Governments and regulated institutions** deploying sovereign AI infrastructure

> If your system ingests external data → TCC sits in front of it.

---

## 🏛️ Part of the Teos Governance Stack

TCC is the data-ingestion layer in the wider Teos ecosystem:

| Layer | Repo | Function |
|---|---|---|
| **1 — Code** | [agent-code-risk-mcp](https://github.com/Elmahrosa/agent-code-risk-mcp) | AI code risk detection |
| **2 — Data** | **teos-comply-crawl** ← you are here | Compliant web ingestion |
| **3 — Pipeline** | [teosmcp-ci-example](https://github.com/Elmahrosa/teosmcp-ci-example) | CI/CD enforcement |
| **4 — Interface** | [teoslinker-bot](https://github.com/Elmahrosa/teoslinker-bot) | Telegram + developer surface |

> TCC is production-oriented as a standalone service today. Cross-repo unification is a roadmap goal, not a claim that all four repos already operate as one deployed platform.

---

## ⚙️ Core Features

### 🔐 PII Pseudonymization
- Detects email, phone, SSN, card-like patterns, and IPv4
- Replaces detected values with stable HMAC-SHA256 pseudonyms
- Raw detected sensitive values are never stored in output
- ReDoS-safe regex, CI-verified on adversarial input

### 🌐 SSRF Protection
- Blocks loopback, private, link-local, and metadata-style targets (including `169.254.169.254`)
- Restricts fetching to `http` / `https` only — `file://`, `gopher://`, `javascript:` blocked
- Re-validates redirects defensively before following

### 🗺️ Crawl Policy
- Enforces `robots.txt` per domain
- Supports per-domain crawl budgets (daily limit, Redis-backed, auto-reset)
- Supports domain concurrency controls to avoid overwhelming targets

### 📊 Auditability
- Job lifecycle tracked through immutable state transitions:
  `PENDING → RUNNING → COMPLETED / BLOCKED / FAILED`
- Stores content hashes and audit-friendly metadata per job
- Designed for traceability and downstream review

### ⚡ Multi-Tenant Billing Foundation
- Atomic credit deduction via Redis (race-condition-free)
- TTL-based plan expiry
- Blocked jobs cost zero credits

---

## ❓ Why Not Just Use a Scraper?

| Risk | Traditional Scraper | TCC |
|---|---|---|
| PII leakage | ❌ possible | ✅ pseudonymized |
| SSRF attacks | ❌ vulnerable | ✅ blocked |
| `robots.txt` | ❌ ignored | ✅ enforced |
| Audit trail | ❌ none | ✅ built-in |
| Compliance readiness | ❌ manual | ✅ structured |
| Blocked request cost | ❌ charged | ✅ free |

TCC is not a scraper — it is a **compliance gate before data ingestion**.

---

## 🚀 Quick Start

### Prerequisites
- Docker + Docker Compose
- `.env` file (copy from `deploy/.env.example`)

```bash
git clone https://github.com/Elmahrosa/teos-comply-crawl.git
cd teos-comply-crawl
cp deploy/.env.example deploy/.env

# Generate secrets — paste into PII_SALT and API_KEY_SALT in .env
python -c "import secrets; print(secrets.token_hex(32))"

docker compose -f deploy/docker-compose.yml up --build
```

---

## 📡 API Reference

### Provision a key (admin)

```bash
curl -X POST http://localhost:8000/internal/provision \
  -H "x-internal-secret: YOUR_INTERNAL_SECRET" \
  -H "Content-Type: application/json" \
  -d '{"api_key":"sk-test","email":"you@example.com","plan":"trial"}'
```

### Submit a URL

```bash
curl -X POST http://localhost:8000/v1/ingest_async \
  -H "X-API-Key: sk-test" \
  -H "Content-Type: application/json" \
  -d '{"url":"https://example.com"}'
```

```json
{"job_id": "550e8400-e29b-41d4-a716-446655440000", "status": "PENDING"}
```

### Check job status

```bash
curl http://localhost:8000/v1/jobs/550e8400-e29b-41d4-a716-446655440000 \
  -H "X-API-Key: sk-test"
```

```json
{
  "job_id": "550e8400-e29b-41d4-a716-446655440000",
  "status": "COMPLETED",
  "domain": "example.com",
  "pii_found": 2,
  "content_hash": "a1b2c3d4...",
  "result_excerpt": "Example Domain. This domain is for...",
  "completed_at": "2026-03-22T10:05:00+00:00"
}
```

### Check account & credits

```bash
curl http://localhost:8000/v1/account \
  -H "X-API-Key: sk-test"
```

### Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/v1/ingest_async` | Submit URL for compliant ingestion |
| `GET` | `/v1/jobs/{job_id}` | Get job status and result |
| `GET` | `/v1/jobs` | List all jobs for API key |
| `GET` | `/v1/account` | Check credits and plan |
| `GET` | `/health` | Health check |
| `POST` | `/internal/provision` | Create API key (admin) |
| `POST` | `/internal/register-key` | Alias — create API key (admin) |
| `POST` | `/internal/expire` | Expire API key (admin) |
| `POST` | `/internal/revoke` | Revoke API key immediately (admin) |

---

## 💳 Pricing

| Plan | Limits | Price |
|---|---|---|
| **Free Trial** | 100 URLs · 14 days | **$0** |
| **Starter** | 10,000 URLs / month | **$29/mo** |
| **Growth** | 75,000 URLs / month | **$129/mo** |
| **Scale** | 250,000 URLs / month | **$299/mo** |
| **Enterprise** | Unlimited + SLA + private deployment | **$1,500+/mo** |

### Credit model

| Action | Cost |
|---|---|
| URL fetch | 1 credit |
| CI code scan | 2 credits |
| Code audit (full) | 5 credits |
| Contract monitoring | 10 credits / day |
| Blocked request | **0 credits** |

### Payments

Supported via:

- **PayPal** → [ayman@teosegypt.com](mailto:ayman@teosegypt.com)
- **USDT (TRC20)** → contact for wallet address
- **Pi Network** → contact for Pi wallet
- **Enterprise invoice** → [ayman@teosegypt.com](mailto:ayman@teosegypt.com)

> Billing can be sold now through manual or semi-automated provisioning. Full billing automation is Phase 2.

### What customers actually buy

Customers are not buying scraping or raw data.

They are buying **risk reduction + auditability**:

- Reduced legal exposure from uncontrolled PII ingestion
- Reduced security risk from SSRF-vulnerable pipelines
- Reduced compliance cost through structured, auditable output

This is why TCC pricing sits above commodity scraping APIs — and why enterprise pricing reaches $1,500+/mo.

---

## ⚖️ Compliance Positioning

TCC is designed to **support** safer governance and evidence collection for:

| Framework | How TCC supports it |
|---|---|
| 🇪🇺 **EU AI Act** | Supports safer data-governance controls during ingestion |
| 🌍 **GDPR** | Supports privacy-by-design through pseudonymization and data minimization |
| 🇺🇸 **NIST AI RMF** | Supports auditability, traceability, and operational risk control |
| 📋 **ISO 42001** | Supports AI management system controls and data quality governance |
| 🇪🇬 **NTRA** | Supports sovereign deployment requirements |

> TCC should be described as **aligned with** or **supporting** these compliance workflows — not as a substitute for legal review or formal certification.

---

## 📄 Enterprise Add-On: Compliance PDF

Planned enterprise reporting package (Phase 2):

- Total URLs ingested and total URLs blocked
- Count of PII items pseudonymized per run
- SSRF attempt log with blocked targets
- Signed content hashes for tamper evidence
- Tenant-scoped activity summary

> Present as **shipped** only after the PDF generator is implemented.

---

## 🧱 Deployment Tiers

### Tier 1 — SaaS *(active)*
Hosted API · credits · onboarding · global access
👉 [teosegypt.com](https://teosegypt.com)

### Tier 2 — IaaS / Self-Hosted
Private Docker deployment · full stack · custom config
💰 **$599/mo**

### Tier 3 — Enterprise / On-Prem
Private deployment · SLA · custom compliance mapping
💰 **$1,500–$5,000+/mo**

### Tier 4 — ZIP / Source License
Full source transfer · deployment stack · 1-year updates · onboarding support
💰 **$15,000–$25,000 one-time**

---

## 🗺️ Execution Roadmap

**Phase 1 — SaaS**
- TCC standalone launch
- Free → Starter → Growth conversion funnel
- Manual / semi-automated provisioning
- GitHub Pages landing + docs

**Phase 2 — Infrastructure**
- Self-hosted Docker package
- Compliance PDF export (enterprise add-on)
- PayPal + crypto billing automation
- Team deployment offer

**Phase 3 — Enterprise / ZIP**
- Private deployment with SLA
- Unified gateway across all four repos
- ZIP / source license at high ticket

---

## 🔒 Security

### SSRF-blocked targets

```
10.0.0.0/8        RFC 1918 private
172.16.0.0/12     RFC 1918 private
192.168.0.0/16    RFC 1918 private
127.0.0.0/8       Loopback
169.254.0.0/16    Link-local / AWS instance metadata
::1/128           IPv6 loopback
file://           Local filesystem access — blocked
gopher://         Internal protocol — blocked
javascript:       Script injection — blocked
```

### PII pseudonymization example

```
Before: "Contact support@example.com or call (555) 123-4567"
After:  "Contact [EMAIL:a1b2c3d4e5f6] or call [PHONE:x9y8z7w6v5u4]"
```

Same input always maps to the same pseudonym. Original is never stored.

### CI security gates (every push)

- `bandit` — Python SAST
- `pip-audit` — dependency vulnerability scan
- ReDoS resistance — all PII regex patterns verified < 1s on adversarial input

### Security notes

- Never commit `.env` files
- Rotate `PII_SALT` and `API_KEY_SALT` on a schedule; treat any exposure as a rotation event
- Prefer PostgreSQL over SQLite in production
- Tenant isolation is a roadmap item — per-tenant salt separation is not yet implemented

---

## ⚙️ Configuration

| Variable | Required | Description |
|---|---|---|
| `PII_SALT` | ✅ | 32-byte hex — HMAC key for PII pseudonymization |
| `API_KEY_SALT` | ✅ | 32-byte hex — HMAC key for API key hashing |
| `DASHBOARD_ADMIN_PASSWORD` | ✅ | Admin dashboard password |
| `GAS_WEBHOOK_SECRET` | ✅ | Billing webhook shared secret |
| `REDIS_URL` | ✅ | `redis://redis:6379/0` |
| `CELERY_BROKER_URL` | ✅ | `redis://redis:6379/1` |
| `CELERY_RESULT_BACKEND` | ✅ | `redis://redis:6379/2` |
| `MAX_RESPONSE_BYTES` | — | Max download per URL (default: 5 MB) |
| `REQUEST_TIMEOUT_SECONDS` | — | HTTP timeout (default: 30s) |
| `ROBOTS_ERROR_MODE` | — | `allow` or `deny` when robots.txt unreachable |

---

## 🗺️ Crawl Policy (`config/rules.yaml`)

```yaml
domains:
  - domain: "wsj.com"
    allow: false
    reason: "paywalled content"

  - domain: "wikipedia.org"
    allow: true
    crawl_budget: 500      # max requests per domain per day
    max_concurrent: 2      # max simultaneous connections

  - domain: "internal.example.com"
    allow: true
    blocked_paths:
      - "/admin"
      - "/api/internal"

default: allow
```

---

## 🧩 MCP Integration

```json
{
  "mcpServers": {
    "teos-comply-crawl": {
      "url": "https://your-host/mcp",
      "headers": { "X-API-Key": "sk-your-key" }
    }
  }
}
```

Available MCP tool: `ingest_url` — submits a URL and returns scrubbed content when complete.

---

## 🧪 Running Tests

```bash
pip install -r requirements-dev.txt

export PII_SALT="0123456789abcdef0123456789abcdef"
export API_KEY_SALT="abcdef0123456789abcdef0123456789"
export DASHBOARD_ADMIN_PASSWORD="supersecure123"
export API_KEY_HASHES_JSON="[]"
export GAS_WEBHOOK_SECRET="test-secret"
export REDIS_URL="redis://localhost:6379/0"
export CELERY_BROKER_URL="redis://localhost:6379/1"
export CELERY_RESULT_BACKEND="redis://localhost:6379/2"

pytest tests/ -v
pytest tests/security/ -v   # SSRF + PII regression only
```

---

## 📁 Project Structure

```
teos-comply-crawl/
├── api/
│   ├── routes/ingest.py        # /v1/ingest_async, /v1/jobs, /internal/*
│   ├── routes/metrics.py       # /metrics
│   ├── dependencies.py         # require_api_key FastAPI dependency
│   └── server.py               # App, middleware, router registration
├── collectors/
│   └── http_connector.py       # SSRF-hardened async HTTP client
├── config/
│   └── rules.yaml              # Domain allow/deny policy
├── core/
│   ├── auth.py                 # API key hashing, Redis storage, credit deduction
│   ├── config.py               # Settings (pydantic-settings)
│   ├── database.py             # SQLAlchemy session management
│   ├── models.py               # Job model, JobStatus enum, state machine
│   ├── pii.py                  # PII patterns, scrub_text(), stable_hash()
│   └── policy.py               # PolicyEngine, CrawlBudget, DomainConcurrency
├── deploy/
│   ├── docker-compose.yml
│   ├── Dockerfile
│   └── .env.example
├── infrastructure/queue/
│   ├── celery_app.py           # Celery app + config
│   └── tasks.py                # ingest_url_task — core worker
├── mcp/
│   └── server.py               # MCP server endpoint
├── scripts/
│   ├── gas_billing_bridge.js   # Google Apps Script billing webhook
│   └── rotate_api_keys.py      # Key rotation utility
└── tests/
    ├── security/
    │   ├── test_pii_regex.py   # ReDoS + accuracy tests
    │   └── test_ssrf_bypass.py # SSRF bypass tests
    └── test_core.py
```

---

## 🚦 Job Status Reference

```
PENDING → RUNNING → COMPLETED
                  ↘ BLOCKED     (policy violation / SSRF attempt)
                  ↘ RETRYING → RUNNING
                             ↘ FAILED
```

Terminal states (`COMPLETED`, `BLOCKED`, `FAILED`) — no further transitions.

---

## 💬 Commercial Contact

TCC is governed by the **TEOS Sovereign License (TESL v2.0)** — see [LICENSE](LICENSE).

- **Non-commercial / research / sovereign government use** → free with attribution
- **Commercial use** → requires a commercial license

📧 **[ayman@teosegypt.com](mailto:ayman@teosegypt.com)**
🌐 **[teosegypt.com](https://teosegypt.com)**

---

<div align="center">

**Built by [Elmahrosa International](https://teosegypt.com) — Egypt**

*Governed by the [International Civic Blockchain Constitution (ICBC)](https://github.com/Elmahrosa/Teos-International-Civic-Blockchain-Constitution)*

**Every commit is a civic milestone.**

© 2026 Elmahrosa International

</div>
