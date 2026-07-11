# TEOS Master Roadmap 2026-H2

> Org project board requires GitHub token scope `project`. This file is the canonical roadmap until Projects V2 is enabled.
> Status: **ACTIVE** · Owner: **NEXUS / SPIKE** · Phase 0 executed: 2026-07-11

## Status legend
- [ ] Backlog
- [~] In progress
- [x] Done

## Phase 0 — Org hygiene (Week 1) CRITICAL
- [x] Create teams: `elmahrosa-exec`, `teos-platform`, `teos-security`, `teos-apps`, `teos-public`
- [x] Assign all org members to teams
- [x] Grant team repo access by pillar
- [x] Branch protection on public P1 repos
- [~] Branch protection on private P1 (blocked: Free plan — needs GitHub Team/Pro or rulesets)
- [x] CODEOWNERS on top 8 P1 repos
- [ ] Create GitHub Project "TEOS Master Roadmap 2026-H2" (needs `project` OAuth scope)
- [ ] Enable org 2FA requirement
- [ ] Secrets rotation review by human

## Phase 1 — Platform spine (Weeks 1–4)
1. `teos-auth-library` — shared JWT/OAuth2 contract
2. `teos-sentinel-shield` + public docs `teos-sovereign-security-stack`
3. `agent-code-risk-mcp` + `teos-forge` CI policy-as-code
4. `teos-mission-control` — founder cockpit deploy
5. `teos-activation-service` — licensing/billing

**DoD:** auth → Sentinel policy → Mission Control status → license activation path works for one vertical.

## Phase 2 — Money + identity MVP (Weeks 3–8)
- Wallet + VC: `teos-sovereign-wallet`, `teos-civic-dpi-vc-sim`
- Payments: `teos-payment-rail`, public showcase `fpbe-bank`
- Custody: `AssetVault` (after Phase 1 gates)
- Defer: `teos-civic-mixer` pending legal review

## Phase 3 — Verticals & GTM (Weeks 5–12)
- Events: `teos-event-site` (ConSensus)
- Healthcare: `UnityCare-Platform`
- Smart city: `teos-pi-smart-city`
- Brand: consolidate `elmahrosa-org` vs `Elmahrosa.github.io`

## Phase 4 — Governed AI (Weeks 8–12)
- `Ask-Teos-AI`, `teos-superintelligence`, `teos-never-died` only via Sentinel/MCP gates

## Pillar map (active repos)
| Pillar | Teams |
|--------|-------|
| Control plane | teos-platform, elmahrosa-exec |
| Security mesh | teos-security, teos-platform |
| Identity & money | teos-platform |
| Vertical apps | teos-apps |
| Growth/commercial | teos-apps, teos-platform |
| Trust/public | teos-public |

## Links
- Teams: https://github.com/orgs/Elmahrosa/teams
- Org: https://github.com/Elmahrosa