# 🔒 Organization REPO_LOCK Policy — Elmahrosa International

## Status
**MANDATORY — ORG-WIDE CONSTITUTIONAL CONTROL**

This policy defines the mandatory **Repository Lock (REPO_LOCK)** baseline for
all repositories under the Elmahrosa GitHub organization.

This is an organizational enforcement policy, subordinate to:
- ICBC (Supreme Charter)
- TEOS-FORGE (Governance Stewardship)
- TESL (Canonical License)

---

## 1) Objective

Every repository must be:
- **Auditable**
- **Authority-safe**
- **Non-forkable in sovereignty claims**
- **Cryptographically fingerprinted (SHA-256)**
- **Governance-controlled (CODEOWNERS + Signed commits)**

---

## 2) Required Files (Org Baseline)

Each repository MUST include:

### Governance & Authority
- `README.md` (standing, chain links, what is/is not)
- `LICENSE.md` (or `LICENSE`) aligned to TESL or explicitly MIT sandbox
- `REPO_LOCK.md` (**canonical hash registry + lock declaration**)
- `SECURITY.md` (or inherit org-wide SECURITY)

### Contribution Control
- `.github/CODEOWNERS` (must include `* @Elmahrosa`)
- `.github/pull_request_template.md` (org or repo-specific)
- `CONTRIBUTING.md` (no forks claiming authority; sign-offs)

### CI Integrity (minimum)
- Markdown lint
- Required file checks (README/SECURITY/REPO_LOCK/LICENSE)
- Optional: link-check for docs-heavy repos

---

## 3) REPO_LOCK Standard (Mandatory Format)

All repositories must implement `REPO_LOCK.md` with:

- Declared status: **LOCKED — CANONICAL** (or **SANDBOX — NON-CANONICAL**)
- Hash standard: SHA-256, UTF-8, lowercase hex
- Canonical registry table including all locked files
- Root-of-Trust list
- Amendment rules requiring:
  1) Governance procedure
  2) Version bump
  3) New hashes
  4) Update registry
  5) Signed commit (GPG or SSH)

---

## 4) Lock Classes

### A) Canonical Sovereign Repos (Must be LOCKED)
These must be constitutionally locked with full hash registry:

- Teos-International-Civic-Blockchain-Constitution (ICBC)
- TEOS-FORGE
- TEOS-Governance
- Elmahrosa-Core
- Teos-Sovereign-System
- TEOS-API-Sovereign

### B) Controlled Modules (LOCKED, but narrower)
Compliance kits, AI guard/auditor, identity, etc.
Lock core specs + manifests; allow docs updates under non-breaking rules.

### C) Sandbox Tools (Explicitly NON-CANONICAL)
If MIT/experimental:
- Must declare **SANDBOX — NON-CANONICAL**
- Must NOT claim authority
- Must NOT reuse TEOS Sovereign badges implying canonical governance

---

## 5) Hash Ceremony Standard (Org Procedure)

All repos must support verification using:

```bash
git ls-files
sha256sum <locked file>
````

For initial locking:

1. Create `REPO_LOCK.md` with placeholders
2. Compute hashes for each locked file
3. Insert hashes + lock date
4. Commit with **signed commit**
5. Push to `main`

Signed commits are mandatory for all changes to Root-of-Trust.

---

## 6) Enforcement Rules (Non-Negotiable)

* No PR may merge without CODEOWNER approval
* No change to Root-of-Trust without hash registry update
* Any fork or derivative claiming sovereign authority is invalid under TESL
* CI must fail if required files are missing

---

## 7) Canonical Authority Chain Reference

All repos must reference the chain:

ICBC → TEOS-FORGE → TEOS-Governance → Elmahrosa-Core → Execution / API

Execution never creates authority.

---

## 8) Contact

**Authority:** Elmahrosa International
📧 [ayman@teosegypt.com](mailto:ayman@teosegypt.com)


```
