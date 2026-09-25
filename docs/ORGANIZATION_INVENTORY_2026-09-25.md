# Elmahrosa International — Canonical Organization Inventory (2026-09-25)

## 1. Generation

- **Generated:** 2026-09-25 19:59:02 UTC
- **Organization:** `Elmahrosa` (Elmahrosa International)
- **Scope:** all repositories visible to an authenticated organization member (public + private)

## 2. Source

- Primary: authenticated GitHub REST API organization repository listing
  `GET /orgs/Elmahrosa/repos?per_page=100&type=all` (fully paginated)
- Cross-check: GraphQL `organization(login:"Elmahrosa").repositories.totalCount`
  → total/public/private = `87/28/59`
- Both sources agree. No estimation or manual adjustment was applied.

## 3. Current counts

| Metric | Count |
| :--- | ---: |
| **Total** | **87** |
| Active (not archived) | 43 |
| Archived | 44 |
| Public | 28 |
| Private | 59 |
| Public + active | 24 |
| Public + archived | 4 |
| Private + active | 19 |
| Private + archived | 40 |

## 4. Arithmetic reconciliation

- `Total = Active + Archived` → 87 = 43 + 44 ✅
- `Total = Public + Private` → 87 = 28 + 59 ✅
- `Active = Public + active + Private + active` → 43 = 24 + 19 ✅
- `Public = Public + active + Public + archived` → 28 = 24 + 4 ✅

## 5. Complete repository table

28 public repositories and 59 private repositories. Only repository-level
metadata is recorded below (name, visibility, archived state, default branch).

| # | Repository | Visibility | Archived | Default branch |
| ---: | :--- | :--- | :--- | :--- |
| 1 | `.github` | public | No | `main` |
| 2 | `Ask-Teos-AI` | public | No | `main` |
| 3 | `AssetVault` | private | No | `main` |
| 4 | `ConSensus-Elmahrosa-Alexandria-Prep` | public | Yes | `main` |
| 5 | `Digital-Reconstruction-of-Gaza` | private | No | `main` |
| 6 | `EGDFESTIVAL` | public | No | `main` |
| 7 | `EGDMENA` | public | No | `main` |
| 8 | `ERT-LAUNCH` | private | Yes | `main` |
| 9 | `ElMahrosa-Pi-Smart-City` | private | Yes | `main` |
| 10 | `Elmahrosa-Blockchain` | private | Yes | `main` |
| 11 | `Elmahrosa-Core` | private | Yes | `main` |
| 12 | `Elmahrosa-Map-of-PI` | private | Yes | `main` |
| 13 | `Elmahrosa-Sovereign-AI-Academy` | public | No | `main` |
| 14 | `Elmahrosa.github.io` | public | No | `main` |
| 15 | `FPBE-First-Pimisr-Bank` | private | Yes | `main` |
| 16 | `Mine_alltokens` | private | Yes | `main` |
| 17 | `Nilex` | private | Yes | `main` |
| 18 | `TEOS-API-Sovereign` | private | Yes | `main` |
| 19 | `TEOS-Egypt-SovereignStack-2026` | private | Yes | `main` |
| 20 | `TEOS-Global-Civic-Blockchain-Ecosystem` | private | Yes | `main` |
| 21 | `TEOS-Governance` | private | Yes | `main` |
| 22 | `TEOS-Identity-Insight-AI` | private | Yes | `main` |
| 23 | `TEOS-NFT-AI-Generator` | private | Yes | `main` |
| 24 | `TEOS-Token-SPL` | private | Yes | `main` |
| 25 | `Teos-Bankchain-Mobile` | private | Yes | `main` |
| 26 | `Teos-Gold-Reserve` | private | Yes | `main` |
| 27 | `Teos-Integration` | private | Yes | `main` |
| 28 | `Teos-Pharaoh-Portal` | private | Yes | `main` |
| 29 | `Teos-Sat-Sovereign-System` | private | Yes | `main` |
| 30 | `Teos-Sovereign-System` | private | Yes | `main` |
| 31 | `TeosEgypt-AI-Travel-OS` | private | Yes | `main` |
| 32 | `TeosEgypt-DomainPlatform` | private | Yes | `main` |
| 33 | `TeosPitaxi` | private | Yes | `main` |
| 34 | `UCH-Backend` | private | Yes | `main` |
| 35 | `UCH-Buyer-Kit` | private | Yes | `main` |
| 36 | `U_C_H2` | public | Yes | `main` |
| 37 | `Unity-Care-Hospital-Sovereign` | private | Yes | `main` |
| 38 | `UnityCare` | public | Yes | `main` |
| 39 | `UnityCare-Platform` | public | No | `main` |
| 40 | `agent-code-risk-mcp` | private | No | `main` |
| 41 | `audit-hub` | public | No | `main` |
| 42 | `demo-repository` | private | Yes | `main` |
| 43 | `elmahrosa-ai-app-store-builder` | public | No | `master` |
| 44 | `elmahrosa-official-website` | public | No | `master` |
| 45 | `elmahrosa-org` | public | No | `main` |
| 46 | `elmahrosa-website` | private | Yes | `main` |
| 47 | `fpbe-bank` | private | No | `main` |
| 48 | `hk-consensus-2026-teos` | private | Yes | `main` |
| 49 | `safe-ingestion-engine` | private | Yes | `main` |
| 50 | `salma-unity-care-hospital` | public | Yes | `main` |
| 51 | `teos-academy` | private | No | `main` |
| 52 | `teos-activation-service` | private | No | `main` |
| 53 | `teos-ai-auditor` | public | No | `main` |
| 54 | `teos-ai-engine` | public | No | `main` |
| 55 | `teos-ai-guard` | public | No | `main` |
| 56 | `teos-app-studio` | private | Yes | `main` |
| 57 | `teos-auth-library` | public | No | `main` |
| 58 | `teos-bankchain` | private | Yes | `main` |
| 59 | `teos-civic-dpi-vc-sim` | private | No | `master` |
| 60 | `teos-civic-mixer` | public | No | `main` |
| 61 | `teos-compliance-kit` | public | No | `main` |
| 62 | `teos-comply-crawl` | private | No | `main` |
| 63 | `teos-dealmaker` | public | No | `main` |
| 64 | `teos-ecosystem-events` | private | Yes | `main` |
| 65 | `teos-ecosystem-launchpad` | private | No | `main` |
| 66 | `teos-ecosystem-mining` | private | Yes | `main` |
| 67 | `teos-ert-token` | public | No | `main` |
| 68 | `teos-event-site` | private | No | `master` |
| 69 | `teos-forge` | public | No | `main` |
| 70 | `teos-international-civic-blockchain-constitution` | public | No | `main` |
| 71 | `teos-labs-due-diligence-mcp` | private | No | `main` |
| 72 | `teos-mission-control` | private | No | `master` |
| 73 | `teos-never-died` | private | No | `main` |
| 74 | `teos-payment-rail` | private | No | `main` |
| 75 | `teos-pi-smart-city` | private | No | `main` |
| 76 | `teos-platform` | private | Yes | `main` |
| 77 | `teos-sentinel-shield` | public | No | `main` |
| 78 | `teos-sentinel-stack` | private | Yes | `master` |
| 79 | `teos-sovereign-security-stack` | private | No | `main` |
| 80 | `teos-sovereign-wallet` | private | No | `main` |
| 81 | `teos-superintelligence` | private | No | `main` |
| 82 | `teos-vap-engine` | private | Yes | `mine` |
| 83 | `teos-video-engine` | public | No | `main` |
| 84 | `teoslinker-bot` | private | No | `main` |
| 85 | `teosmcp-ci-example` | public | No | `main` |
| 86 | `uch-sovereign-core` | private | Yes | `main` |
| 87 | `x-teos-pro` | private | Yes | `main` |

## 6. Interpretation notes

- **`87` is the TOTAL repository count. It is not a public count.**
  The public repository count is **28**.
- The count of public **and** non-archived repositories is **24**; all 24 were
  verified to have branch protection enabled on their default branch on
  2026-09-25.

## 7. Comparability statement

These figures describe the verified organization state on 2026-09-25. Historical repository counts in older documents are not automatically comparable because repository transfers, deletions, renames, and archival state changes can affect historical reconstruction.
