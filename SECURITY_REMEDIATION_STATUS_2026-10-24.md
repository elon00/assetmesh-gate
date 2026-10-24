# Assetmesh Gate — fail-closed CI remediation checkpoint (2026-10-24)

Scope: original owner `elon00`, canonical manifest ID `QMOOSA-0710` (Batch 142, tests component). This document records **unverified** security posture; it is not an approval.

## Observed GitHub Actions failures

- Main-HEAD run 40058195620: `CodeQL Analysis` failed with "Config file could not be found at expected location. Has the 'init' action been called?" The separate CI workflow invoked `github/codeql-action/analyze@v3` without first running CodeQL init.
- Legacy `.github/workflows/codeql.yml` uses invalid action refs `actions/checkout@4`, `github/codeql-action/init@3` and `github/codeql-action/analyze@3`.
- `tests/reality_battery.py` contains a U+0004 control character and malformed Python. It must not be skipped or deleted to manufacture a passing CI result.
- `tests/reality_check_harness.py` contains placeholder assertions and self-reported `100/100` claims. It does not exercise the approved metaverse protocol/engine, external relayer, cryptographic implementation, or deployment.

## Remediation on this review branch

1. CI invokes `compileall` and `pytest` and fails if either fails.
2. CodeQL is initialized for the actual Python language with valid `@v3` action references and separate analysis.
3. Unverified `100/100 VERIFIED` echo is removed from the workflow.

## Unresolved blockers / acceptance criteria

- Replace corrupted tests with genuine implementation-coupled regression tests **after identifying and reviewing the real protocol/engine APIs**; include negative/adversarial cases and run them in CI.
- Remove or qualify misleading production/PQC/reality-gate claims in source/docs, with evidence.
- Obtain green checks on the PR head and on default-branch HEAD after an authorized review/merge.
- Independent security review and deployment gates are required separately. Neither is claimed here.
- Approved manifest marks this component `private: true`, but GitHub currently exposes it publicly. Resolve visibility policy after a sensitive-data review; do not automatically toggle visibility.

No secrets, network deployments, paid resources, force pushes or merges are part of this remediation.
