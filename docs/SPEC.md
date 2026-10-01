# SPEC — Solution Deal Agent FAST DEMO

Status: DRAFT  
Mode: FAST DEMO  
Method: PA-SDD / Minimum Sufficient Specification

## 1. Business intent

Pre-sales and solution-design work is often fragmented across people, documents, historical proposals, architecture standards, pricing spreadsheets and manual artifact creation.

Solution Deal Agent will demonstrate that an agentic system can convert an opportunity or RFP into a structured, traceable deal definition and assist specialists through design, estimation, pricing, validation and proposal generation.

The FAST DEMO is intended to prove the behavior and value proposition, not to reproduce every enterprise integration or production control.

## 2. North Star

**Median time from qualified opportunity to validated proposal-ready package.**

Guardrails:
- critical-source traceability;
- architecture-decision traceability;
- estimate transparency;
- commercial consistency;
- human approval.

## 3. Scope — FAST DEMO

In scope:

1. Conversational creation of an opportunity.
2. Upload and analysis of one RFP/RFI-style document.
3. Extraction and classification of requirements.
4. Explicit known / unknown / assumed status.
5. Clarification questions for missing material information.
6. Persistent Deal Spec.
7. Retrieval of mock/demo precedents from a knowledge base.
8. Retrieval of governed demo architecture policies/patterns.
9. Architecture proposal with rationale and references.
10. WBS / role / FTE / hour estimation.
11. Deterministic demo cost/price calculation.
12. Independent validation of consistency and missing evidence.
13. Generation of at least one proposal artifact.
14. Human approval before final proposal-ready state.
15. Basic trace/evidence log for important decisions.

## 4. Out of scope — FAST DEMO

- production CRM integration;
- enterprise ERP integration;
- production rate-card system integration;
- real confidential customer data;
- automated binding commercial commitments;
- automatic sending of proposals to clients;
- production-grade legal review;
- full identity federation / enterprise SSO;
- full private networking topology;
- full GraphRAG / enterprise knowledge graph;
- autonomous final approval;
- full delivery actuals integration;
- all commercial document formats.

## 5. Personas

### P-001 — Sales / Pre-sales
Needs to initiate and progress an opportunity quickly.

### P-002 — Architect
Needs reliable context, reusable standards and evidence to create solution decisions.

### P-003 — Commercial / Pricing specialist
Needs effort inputs and deterministic calculation rules.

### P-004 — Proposal reviewer / approver
Needs completeness, consistency and traceability before approval.

### P-005 — Knowledge curator
Maintains approved architecture patterns, standards or reference content.

## 6. Critical user stories

### US-001 — Start opportunity conversationally
As a pre-sales user, I want to describe an opportunity conversationally so that the platform structures the available context and asks for missing information.

### US-002 — Upload RFP
As a pre-sales user, I want to upload an RFP so that requirements are extracted, classified and traced to their source.

### US-003 — Produce traceable architecture
As an architect, I want the system to combine requirements, approved architecture knowledge and precedents so that I can review a proposed solution with explicit rationale.

### US-004 — Estimate effort and price
As a commercial team member, I want approved scope/design to be converted into effort and a deterministic pricing result so that the basis of the proposal is transparent.

### US-005 — Validate and generate proposal
As a reviewer, I want the system to detect gaps and inconsistencies before generating the proposal artifact so that I can approve an evidence-backed package.

## 7. Functional requirements

### Intake / RFP

**FR-001** The system shall allow a user to create a new deal by conversation.

**FR-002** The system shall allow a user to upload an RFP/RFI-style document supported by the demo parser.

**FR-003** The system shall extract candidate requirements from the uploaded document.

**FR-004** The system shall classify requirements at minimum into business, functional, non-functional, security, architecture, commercial and delivery categories where applicable.

**FR-005** The system shall preserve a source reference for extracted RFP requirements.

**FR-006** The system shall identify missing or ambiguous material information and generate clarification questions.

### Deal Spec

**FR-007** The system shall maintain one canonical Deal Spec per opportunity.

**FR-008** The Deal Spec shall distinguish confirmed, assumed, unknown and derived information.

**FR-009** Specialist outputs shall update or reference the Deal Spec rather than create independent conflicting state.

### Knowledge / precedents

**FR-010** The system shall retrieve relevant historical/demo precedents using semantic and/or metadata retrieval.

**FR-011** Retrieved precedent evidence shall expose its source identifier and relevant metadata.

**FR-012** The system shall retrieve approved demo architecture policies/patterns separately from historical proposal evidence.

### Architecture

**FR-013** The Architect Agent shall use current requirements, governed architecture knowledge and relevant precedents as distinct evidence classes.

**FR-014** The Architect Agent shall ask for clarification when a material design decision lacks sufficient information.

**FR-015** The Architect Agent shall provide at least one proposed technical solution with rationale, assumptions, trade-offs and cited evidence.

**FR-016** Material architecture decisions shall be recorded in a structured decision form / ADR-like record.

### Estimation / pricing

**FR-017** The Estimator Agent shall generate a WBS or activity list linked to the proposed solution.

**FR-018** The Estimator Agent shall propose roles, FTE/hours and duration assumptions.

**FR-019** The estimate shall identify the precedent, rule or assumption used for material effort values.

**FR-020** Pricing shall be calculated by a deterministic tool from structured effort and demo commercial rules.

**FR-021** The pricing result shall expose calculation inputs and outputs.

### Validation / artifacts

**FR-022** The Validator Agent shall evaluate completeness, evidence traceability and cross-artifact consistency.

**FR-023** The validator shall identify unresolved critical issues before proposal-ready status.

**FR-024** The system shall generate at least one proposal artifact from the approved Deal Spec.

**FR-025** The generated artifact shall not silently override approved Deal Spec values.

### Approval

**FR-026** The system shall require explicit human approval before changing a deal to PROPOSAL_READY.

**FR-027** Approval shall record actor, timestamp, decision and relevant validation summary in demo state.

## 8. Business rules

**BR-001** Missing critical information must be surfaced as unknown or assumed; it must not be silently invented.

**BR-002** Historical prices and effort are references, not authoritative current-deal values.

**BR-003** Deterministic commercial calculations must run through a tool/rule function, not free-form LLM arithmetic.

**BR-004** Architecture recommendations must reference at least one current requirement and, when available, an approved policy/pattern or explicit precedent.

**BR-005** A proposal cannot become PROPOSAL_READY while critical validator findings remain unresolved unless a human explicitly accepts the exception.

**BR-006** Human approval remains authoritative for final proposal readiness.

**BR-007** Every generated artifact uses the same canonical Deal Spec version.

## 9. Logical data model

```text
User
 └──< Deal
       ├──< SourceDocument
       │     └──< SourceFragment
       ├──< Requirement
       ├──< Clarification
       ├──< Assumption
       ├──< EvidenceReference
       ├──< Precedent
       ├──< ArchitectureDecision
       ├──  ArchitectureSolution
       ├──< WorkItem / WBSItem
       ├──< EffortEstimate
       ├──  PricingCalculation
       ├──< ValidationFinding
       ├──< Artifact
       └──< Approval
```

Minimum Deal state:

```text
DRAFT
→ DISCOVERY
→ DESIGN
→ ESTIMATION
→ VALIDATION
→ PROPOSAL_READY
→ WON / LOST
```

## 10. Agentic extension

### Orchestrator contract

The orchestrator:
- owns lifecycle coordination;
- reads/writes only through explicit Deal Spec services/tools;
- delegates specialist analysis;
- does not bypass required validation/approval gates;
- communicates missing information to the user.

### Specialist contracts

Initial logical specialists:
- Intake Agent;
- Knowledge / Precedent Agent;
- Architect Agent;
- Estimator Agent;
- Validator Agent;
- Artifact Agent.

Pricing may be exposed as an agent-facing deterministic tool rather than a fully autonomous agent in FAST DEMO.

### Knowledge strategy

Separate indexes / collections or metadata classes for:
1. current opportunity sources;
2. reusable architecture knowledge;
3. historical precedents.

### Context strategy

The active Deal Spec is the primary working context. Retrieved knowledge should be scoped to the current task and references preserved.

### Memory strategy

FAST DEMO does not rely on unbounded conversational memory as authoritative business state. Durable deal state is stored explicitly.

### Human approval

Required before PROPOSAL_READY.

### Evals

At minimum:
- RFP requirement extraction sample;
- source citation correctness sample;
- architecture evidence adherence sample;
- estimator schema completeness;
- validator detection of seeded inconsistency;
- deterministic pricing regression test.

## 11. Acceptance criteria — critical flow

### AC-001 — RFP ingestion

Given a supported RFP document
When the user uploads it
Then the system creates or updates a Deal Spec
And extracts candidate requirements
And preserves source references
And identifies at least the intentionally omitted/ambiguous critical fields in the demo fixture.

### AC-002 — Architecture traceability

Given structured requirements and curated architecture knowledge
When architecture analysis is requested
Then the system proposes a solution
And records assumptions
And cites the evidence used for material decisions
And asks for clarification instead of inventing a configured critical unknown.

### AC-003 — Estimate and pricing

Given an approved demo architecture
When estimation and pricing run
Then a structured WBS/effort estimate is created
And the deterministic pricing tool calculates cost and price
And calculation inputs are inspectable.

### AC-004 — Validation

Given a Deal Spec with a seeded inconsistency
When validation runs
Then the system reports the inconsistency
And prevents clean proposal-ready status until it is resolved or explicitly accepted.

### AC-005 — Artifact consistency

Given an approved Deal Spec version
When a proposal artifact is generated
Then the artifact uses the same approved scope, duration and price values
And records the Deal Spec version used.

## 12. Demo success metric

The demo passes when one representative opportunity can complete the critical flow end-to-end with:

- uploaded RFP or conversational intake;
- traceable structured requirements;
- precedent retrieval;
- architecture recommendation with evidence;
- effort estimate;
- deterministic price calculation;
- validator result;
- human approval;
- generated proposal artifact.

## 13. Open decisions

To be resolved before implementation expands:

- exact frontend technology;
- demo persistence choice: Cloud SQL vs simpler managed persistence where sufficient;
- document storage and extraction implementation;
- vector retrieval implementation;
- target artifact format for first demo;
- whether the first demo exposes all specialists explicitly in UI or keeps them behind one orchestrator;
- exact pricing fixture and demo rate-card model;
- authentication scope for FAST DEMO.
