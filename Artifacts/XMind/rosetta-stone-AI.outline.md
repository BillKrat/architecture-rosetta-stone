# rosetta-stone-AI — frozen outline snapshot

Plain-text mirror of `rosetta-stone-AI.xmind` (Concern A: the AI-system
Responsibility vocabulary — the actual Rosetta Stone content), captured at
freeze time on 2026-07-12, immediately after the bullet-prefix cleanup and
the Concern A / Concern B split. The `.xmind` file is the source of record;
this file exists so the frozen content is diffable and readable directly in
git, per the project's persistence convention (see
`Topics/xmind-copilot-collaboration.md`).

This document is frozen: no further edits until comprehensive human review
is complete (see `Sessions/2026-07-12_Checkpoint_0002_...` for the freeze
decision).

---

## AI

### Application

- Responsibilities: Map model/agent outputs to user-facing actions; enforce UI/UX guardrails; present uncertainty and explanations; collect user feedback.
- Collaborators: Agent, Model, Tools, Memory, Retrieval, Security, Product/Design, Human reviewers.
- Inputs / Outputs: Input: model/agent results, user input, context; Output: rendered UI, API responses, user-visible logs, feedback.
- Metrics & Thresholds: User satisfaction (NPS), task completion, error rate, latency to first meaningful response.
- Known Failure Modes: Misleading presentation of confidence, poor error handling, exposing raw model outputs, UX that encourages unsafe actions.
- Runtime Hooks: User feedback capture, display of provenance/confidence, escalation UI for human review.
- Regulatory Notes: Required disclosures, consent flows, accessibility and localization requirements.
- Owner: Product/Application owner.
- Acceptance Criteria: Usability tests, safety UX checks, feedback loop integration.
- Quantitative Thresholds: user_sat_pct >= 70; task_completion_pct >= 85; latency_first_meaningful_ms <= 800.
- Runbook / Dashboard: usability_pass=true; safety_checks_pass=true; feedback_loop_integrated=true; runbook_id=RB-APP-01; dashboard=DB-APP-01.

### Model

- Responsibilities: Process inputs into reliable outputs; declare intended use and limits; expose performance metrics and failure modes; support traceability and versioning; surface uncertainty.
- Collaborators: Data (train/eval), Retrieval, Memory, Agent/Orchestrator, Application/UI, Security/Governance, Human reviewers.
- Inputs / Outputs: Input: tokenized text/embeddings/structured features; Output: predictions, generations, scores, confidences, provenance IDs.
- Metrics & Thresholds: Primary metrics (accuracy/F1/ROUGE/EM), calibration, latency, throughput, segment-level fairness thresholds.
- Known Failure Modes: Hallucination, bias on slices, OOD degradation, calibration drift, adversarial inputs.
- Runtime Hooks: Version id, request id, confidence score, explainability payload, telemetry events, audit logs.
- Regulatory Notes: Model card, risk assessment, allowed/disallowed uses, data provenance disclosure.
- Owner: Model owner/team contact.
- Acceptance Criteria: Evaluation dataset pass rates, safety checks, latency and cost budgets.
- Quantitative Thresholds: accuracy_pct >= 82; f1 >= 0.80; calibration_ece <= 0.05; latency_p95_ms <= 300; throughput_rps >= 100.
- Runbook / Dashboard: accuracy_pct>=82; hallucination_rate_pct<=2; latency_p95_ms<=300; telemetry_coverage=true; model_card=model_card.md; runbook_id=RB-MODEL-01; dashboard=DB-MODEL-01.

#### Model (API-service)

(leaf — no further breakdown yet)

#### Model (Edge)

(leaf — no further breakdown yet)

#### Model (RAG)

- Responsibilities: Combine retrieved context with generative model outputs; attach provenance for each claim; decide when to request more retrieval or escalate to human review.
- Collaborators: Retrieval/index service, Re-ranker, Agent/orchestrator, Memory, Application/UI, Security/Governance, Human-in-loop.
- Inputs / Outputs: Input: user query + retrieved docs/snippets + context embeddings; Output: grounded generation, cited provenance IDs, retrieval confidence, hallucination risk score.
- Metrics & Thresholds: Retrieval recall@k, grounding precision (claims supported by sources), hallucination rate, end-to-end latency, provenance completeness.
- Known Failure Modes: Over-reliance on low-quality retrieval, mismatched provenance, hallucinated claims despite retrieved context, stale sources.
- Runtime Hooks: Retrieval confidence, provenance links in response, re-retrieval triggers, human-review flags when grounding confidence below threshold.
- Regulatory Notes: Source attribution requirements, takedown handling, sensitive-source filtering, logging of provenance for audits.
- Owner: RAG pipeline owner.
- Acceptance Criteria: Grounding precision thresholds met, provenance attached for all factual claims, re-retrieval and escalation behavior validated.
- Quantitative Thresholds: retrieval_recall_at_10 >= 0.85; grounding_precision_pct >= 90; hallucination_rate_pct <= 1; end_to_end_latency_ms <= 800.
- Runbook / Dashboard: grounding_precision>=90; provenance_attached_for_factual_claims=true; re-retrieval_triggers_validated=true; runbook_id=RB-RAG-01; dashboard=DB-RAG-01.

### Agent

- Responsibilities: Decompose goals into steps; select/sequence tools and models; manage retries/fallbacks; maintain task state; escalate to humans when needed.
- Collaborators: Models, Tools, Retrieval, Memory, Application/UI, Security, Human-in-loop.
- Inputs / Outputs: Input: user goal, constraints, context; Output: ordered actions, tool calls, final aggregated result.
- Metrics & Thresholds: Task success rate, average steps per task, time-to-completion, human escalation rate.
- Known Failure Modes: Planning loops, incorrect decomposition, over-reliance on single tool, state inconsistency.
- Runtime Hooks: Step-level logs, action traces, human-review triggers, circuit-breakers.
- Regulatory Notes: Audit trail for autonomous decisions, explainability requirements.
- Owner: Agent owner/team contact.
- Acceptance Criteria: End-to-end task completion SLA, safe-fallback behavior, auditability.

### Tool

- Responsibilities: Execute a single well-defined action (search, API call, calculator); validate inputs; sanitize outputs; declare cost/latency/permissions.
- Collaborators: Agent/Orchestrator, Model, Application, Security, Monitoring.
- Inputs / Outputs: Input: typed parameters or payload; Output: structured result, status code, provenance.
- Metrics & Thresholds: Latency, availability, error rate, cost per call, quota usage.
- Known Failure Modes: Schema mismatch, unhandled exceptions, permission denials, inconsistent outputs.
- Runtime Hooks: Per-call tracing, quota enforcement, circuit-breaker signals, retry policy.
- Regulatory Notes: Data residency, PII handling, contractual constraints.
- Owner: Tool owner/service contact.
- Acceptance Criteria: Schema contract tests, SLA, safe-failure behavior.

### Retrieval

- Responsibilities: Index and return relevant context; rank and score candidates; maintain freshness and deletions; provide provenance.
- Collaborators: Models (RAG), Data pipelines, Memory, Application, Security.
- Inputs / Outputs: Input: query text or embedding; Output: ranked documents/snippets, scores, provenance IDs.
- Metrics & Thresholds: Recall@k, precision, MRR, latency, staleness window.
- Known Failure Modes: Returning stale or irrelevant context, noisy matches that cause hallucination, missing provenance.
- Runtime Hooks: Retrieval confidence, provenance links, re-ranking signals, TTL enforcement.
- Regulatory Notes: Source attribution, takedown/DMCA handling, sensitive-data filters.
- Owner: Retrieval/index owner.
- Acceptance Criteria: Retrieval quality thresholds, freshness guarantees, provenance completeness.

### Memory

- Responsibilities: Store and serve session and long-term user state; enforce access controls, consent, TTL, and selective forgetting.
- Collaborators: Agent, Model, Application/UI, Security/Governance, Human reviewers.
- Inputs / Outputs: Input: structured facts, preferences, session state; Output: contextual attributes, embeddings, consent flags.
- Metrics & Thresholds: Hit rate, staleness, consent compliance, storage cost.
- Known Failure Modes: Privacy leaks, stale or conflicting facts, unauthorized access, incorrect merges.
- Runtime Hooks: Audit logs, consent metadata, redaction endpoints, versioning.
- Regulatory Notes: GDPR/CCPA considerations, user data export/delete, consent records.
- Owner: Memory service owner.
- Acceptance Criteria: Consent enforcement tests, redaction capability, access control audits.

### Security

- Responsibilities: Authenticate and authorize access; enforce data and usage policies; monitor misuse; define incident response and forensics.
- Collaborators: All nodes (Agent, Model, Tool, Memory, Retrieval, Application), Legal, Ops, Compliance.
- Inputs / Outputs: Input: access requests, telemetry, alerts; Output: allow/deny decisions, alerts, audit records, quarantine actions.
- Metrics & Thresholds: Unauthorized access attempts, policy violation rate, time-to-detect, mean-time-to-remediate.
- Known Failure Modes: Misconfigured ACLs, insufficient telemetry, delayed detection, privilege escalation.
- Runtime Hooks: Real-time alerts, quarantine endpoints, forensics logs, policy enforcement points.
- Regulatory Notes: Incident reporting obligations, data breach procedures, encryption and key management.
- Owner: Security/Governance lead.
- Acceptance Criteria: Pen-test pass, monitoring coverage, incident response SLA.

### Deployment Context Notes (API-service / Edge / RAG)

- API-service Responsibilities: Serve model/agent via authenticated endpoints; enforce quotas, rate limits, and centralized telemetry.
- Edge Responsibilities: Run lightweight models locally; enforce privacy-by-design, low-latency constraints, and model update mechanisms.
- RAG Responsibilities: Combine retrieval results with model generation; ensure provenance is attached and retrieval quality is monitored.
- Shared Considerations: Define which responsibilities shift (latency, privacy, freshness); update acceptance criteria and telemetry per deployment type.
- Owner: Deployment owner (infra/devops).
- Acceptance Criteria: Deployment-specific SLAs, update/rollback procedures, security posture.

### Cross-cutting fields to paste into each node if desired

- Owner: Team / contact
- Acceptance Criteria: Concrete pass/fail checks
- SLA / SLO: Latency, availability, cost budgets
- Documentation: Model card, runbook, incident playbook
- Oncall: Pager / escalation path

### Diagnostics / Observability

- Responsibilities: Centralized telemetry, traces, logs, health checks; map metric keys to dashboards; runbook links; alerting.
- Metrics & Thresholds: telemetry_coverage_pct = 100; trace_sampling_rate_pct >= 10; alert_time_to_ack_minutes <= 15.
- Acceptance Criteria: telemetry_coverage_100pct=true; dashboards_link=DB-OBS-01; runbook_id=RB-OBS-01.
