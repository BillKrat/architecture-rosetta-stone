# rosetta-stone-MCP-Bridge — frozen outline snapshot

Plain-text mirror of `rosetta-stone-MCP-Bridge.xmind` (Concern B: the MCP
IDE-extension delivery architecture — build/ship mechanics for a specific
MCP-based host/bridge tool, split out of the original `rosetta-stone-AI`
document on 2026-07-12 because it is a distinct implementation concern, not
part of the general AI-system Responsibility vocabulary). The `.xmind` file
is the source of record; this file exists so the frozen content is diffable
and readable directly in git, per the project's persistence convention (see
`Topics/xmind-copilot-collaboration.md`).

This document is frozen: no further edits until comprehensive human review
is complete (see `Sessions/2026-07-12_Checkpoint_0002_...` for the freeze
decision).

---

## AI

### Transport (MCP / stdio / named-pipe)

- Responsibilities: Reliable IPC; authenticate local clients; enforce message schema and timeouts; support retries and backpressure.
- Metrics & Thresholds: message_schema_valid_pct = 100; connect_timeout_ms <= 2000; message_loss_rate_pct <= 0.01; avg_rtt_ms <= 50 (local).
- Acceptance Criteria: message_schema_valid=true; connect_timeout_ms<=2000; transport_tests_pass=true; runbook_id=RB-TRANSPORT-01; dashboard=DB-TRANSPORT-01.

### Host (VSIX / IDE)

- Responsibilities: Own IDE APIs and editor state; enforce local permission boundaries; present approval UX; schema example: {documentId:string, selectionRange:{start:int,end:int}}.
- Metrics & Thresholds: vsix_unit_tests_pass=true; named_pipe_connectivity_success_pct >= 99; approval_ui_latency_ms <= 300.
- Acceptance Criteria: vsix_tests_pass=true; named_pipe_connectivity=true; runbook_id=RB-HOST-01; dashboard=DB-HOST-01.

### Testing / CI

- Responsibilities: Unit/integration tests, MCP stdio validation, contract tests, CI gating, canary rollouts.
- Metrics & Thresholds: test_coverage_pct >= 80; ci_pipeline_green=true; contract_tests_pass_pct = 100.
- Acceptance Criteria: all_tests_pass=true; ci_pipeline_green=true; canary_success_rate >= 99; runbook_id=RB-CI-01; dashboard=DB-CI-01.

### Packaging / Release

- Responsibilities: Build VSIX, sign artifacts, produce release notes, validate rollback procedures, publish artifacts.
- Metrics & Thresholds: signed_vsix=true; release_verification_pass_pct = 100; rollback_test_success_pct >= 99.
- Acceptance Criteria: signed_vsix=true; release_playbook=RB-REL-01; rollback_validated=true; dashboard=DB-REL-01.

### Connector / Adapter

- Responsibilities: Translate host APIs to MCP tools; maintain schema contracts; manage version compatibility and compatibility matrix.
- Metrics & Thresholds: contract_tests_pass_pct = 100; compatibility_matrix_updated_on_release=true.
- Acceptance Criteria: contract_tests_pass=true; compatibility_matrix_updated=true; runbook_id=RB-CONN-01; dashboard=DB-CONN-01.
