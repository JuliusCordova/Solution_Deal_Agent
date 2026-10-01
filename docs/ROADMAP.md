# Roadmap — Solution Deal Agent

Status: DRAFT

## Phase 0 — Product definition
Goal: establish the minimum sufficient definition before implementation.

Deliverables:
- README / product narrative;
- FAST DEMO SPEC;
- initial logical architecture;
- initial agent/tool contracts;
- demo success criteria;
- representative demo fixture/RFP;
- pricing fixture;
- curated sample architecture knowledge;
- curated sample historical precedents.

Exit gate: critical flow is testable on paper, open decisions are explicit, and no pricing or architecture assumptions remain hidden.

## Phase 1 — FAST DEMO: Deal intake + RFP
Goal: prove that the orchestrator can create a Deal Spec from conversation or an uploaded RFP.

Capabilities: conversational deal creation, RFP upload, requirement extraction/classification, source traceability, known/unknown/assumed classification, clarification questions, and persistent Deal Spec.

Evidence: one golden RFP fixture, expected requirement set, extraction/citation checks, and smoke test.

## Phase 2 — FAST DEMO: Knowledge + Architect
Goal: prove reusable governed knowledge and traceable architecture reasoning.

Capabilities: architecture knowledge ingestion, precedent ingestion, semantic/metadata retrieval, Architect Agent, architecture decision records, alternative/trade-off explanation, and missing-information loop.

Evidence: golden architecture scenario, expected policy/pattern references, negative case with insufficient information, and source-grounding eval.

## Phase 3 — FAST DEMO: Estimation + deterministic pricing
Goal: prove transparent economics without allowing the LLM to invent commercial outputs.

Capabilities: WBS generation, role/FTE/hour estimate, precedent/rule rationale, demo rate-card configuration, deterministic pricing calculator, and inspectable calculation breakdown.

Evidence: pricing regression test, estimate schema test, and reproducibility check.

## Phase 4 — FAST DEMO: Validation + artifact
Goal: prove an end-to-end proposal-ready flow.

Capabilities: Validator Agent, seeded inconsistency detection, readiness status, human approval, generation of first proposal artifact from Deal Spec, and artifact consistency check.

Evidence: validator catches intentional inconsistency, proposal uses canonical Deal Spec values, and approved flow completes end-to-end.

## FAST DEMO exit criteria
A representative opportunity can move through:

```text
RFP / Conversation
→ Deal Spec
→ Precedents
→ Architecture
→ Effort
→ Pricing
→ Validation
→ Human Approval
→ Proposal Artifact
```

with inspectable evidence at every material step.

## MVP horizon
Once FAST DEMO value is proven: production-like UI/API separation, enterprise authentication, robust document ingestion, structured persistence, scalable semantic retrieval, richer rate-card governance, CI/CD, automated evals, observability, enterprise integration contracts, durable approval workflow, multiple artifact templates, and Won/Lost feedback capture.

## PRODUCT horizon
Potential future capabilities: enterprise knowledge governance, versioned architecture-policy lifecycle, multi-business-unit pricing rule packs, estimate-vs-actual learning loop, delivery handoff/PCR automation, GraphRAG/knowledge graph where justified, AgentOps/FinOps, policy-aware agent/tool permissions, private connectivity, event-driven execution, release evidence packs, and MCP/A2A interoperability where justified.

## Product evolution principle
> Add architecture, infrastructure and process only when they reduce ambiguity, risk, rework, operational uncertainty or future change cost.
