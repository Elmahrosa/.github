# CLAUDE.md — Elmahrosa International / TEOS (Organization Baseline)

You operate in repositories stewarded by Elmahrosa International ("TEOS").
This baseline is subordinate to the constitutional chain (ICBC →
TEOS-FORGE → TEOS-Governance → Elmahrosa-Core → Execution/API) and to each
repository's maintainer rules (`AGENTS.md`/`CLAUDE.md` per repository) and
existing org policy documents.

## Authority and licensing

- Law over code: nothing here or in code may claim authority the constitution
  does not confer. Forking does not confer legitimacy.
- Dual-license framework per `NOTICE.md`: PolyForm Noncommercial 1.0.0
  (non-commercial) and TESL (commercial/government/institutional). Canonical
  TESL: https://github.com/Elmahrosa/Teos-Pharaoh-Portal/blob/main/TESL.md
- Preserve required MIT attributions in `THIRD-PARTY-NOTICES` where MIT
  components exist.

## Mandatory repository baseline (REPO_LOCK_POLICY.md)

Before treating a repo as compliant, verify presence: `README.md`, `LICENSE`
(`LICENSE.md`) aligned to TESL or an explicit MIT sandbox, `REPO_LOCK.md`
(canonical hash registry with declared status `LOCKED — CANONICAL/SANDBOX` or
`NON-CANONICAL`), `SECURITY.md`, `.github/CODEOWNERS` including `* @Elmahrosa`,
`.github/pull_request_template.md`, `CONTRIBUTING.md`, and minimum CI (markdown
lint + required-file checks). Absence is a finding, not a reason to skip the
policy.

## Evidence-based claims (mandatory vocabulary)

Classify every material feature claim as exactly one of: VERIFIED (implementation
or reproducible test evidence), PARTIALLY VERIFIED (stated limitations), PLANNED
(not implemented), EXPERIMENTAL (no production acceptance), FAILED (a required
check failed), UNKNOWN (insufficient evidence). Documentation claims are not
implementation evidence: check code and tests first.

## Sentinel Shield rule (where the repo uses Sentinel)

- Inspect the actual enforcement path, policy configuration, tests, and failure
  behavior. A returned verdict is NOT proof of protection.
- Prove that denied operations cannot execute through alternate code paths
  (fallbacks, retries, reflection, bptool/echo paths).
- Sentinel unavailable/invalid/timed-out/unrecognized → fail closed for
  protected or side-effecting operations. Never silently bypass.
- Do not assume Sentinel is installed or effective in every repository.

## Security rules (non-negotiable)

- Least privilege: request only the permissions needed for the current task.
- Never expose, commit, or unnecessarily process tokens, keys, credentials, or
  sensitive user data. Audit logs record decisions without secrets.
- Never push to a default branch, merge, deploy, or change permissions/secrets
  without explicit owner approval — die on stop conditions: unexpected merge,
  destructive action, instruction conflict, or a failing security check.

## Governance & process

- TEOS AI product identity only. Implementation details of the internal agent
  service are not public documentation.
- Preserve unrelated local changes. Present evidence on conflicts before
  proceeding; never overwrite existing instruction files.