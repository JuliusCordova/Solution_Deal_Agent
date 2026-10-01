# Solution Deal Agent

> Agentic Deal Intelligence Platform for turning opportunities, RFPs, requirements and reusable enterprise knowledge into traceable technical solutions, effort estimates, commercial outputs and proposal artifacts.

## 1. Product vision

Solution Deal Agent is a conversational agentic platform that assists the full pre-sales / solution-design lifecycle.

It does **not** aim to replace Solution Architects, Data Architects, DevOps/DevSecOps Architects, Sales or Pricing specialists. Its purpose is to augment them with reusable knowledge, structured reasoning, traceability, deterministic calculations and human approval gates.

The platform should help move an opportunity through the following lifecycle:

```text
Opportunity / RFP / Client Need
        ↓
Understand & Structure
        ↓
Find Precedents
        ↓
Design Solution
        ↓
Estimate Effort
        ↓
Calculate Cost / Price
        ↓
Validate
        ↓
Generate Artifacts
        ↓
Human Approval
        ↓
Won / Lost
        ↓
Knowledge Feedback Loop
```

## 2. North Star

> **Reduce the cycle time required to produce a high-quality, traceable and commercially consistent proposal while preserving human accountability.**

Primary North Star metric:

**Median time from qualified opportunity to validated proposal-ready package.**

The metric must always be read together with quality guardrails so that speed is never optimized at the expense of correctness.

### Quality guardrails

- % of critical claims with traceable source/evidence.
- % of architecture decisions linked to requirements, policies or precedents.
- % of estimates with explicit assumptions and calculation basis.
- proposal consistency across technical scope, effort, price and generated artifacts.
- human validation / approval rate.
- estimate-vs-actual variance when delivery actuals become available.

## 3. Business objectives

1. Reduce repetitive work in pre-sales and solution design.
2. Reuse validated knowledge from historical proposals and enterprise architecture standards.
3. Improve consistency between requirement, technical design, effort, cost, price and commercial documentation.
4. Make architectural and commercial reasoning traceable.
5. Capture expert knowledge as reusable governed assets.
6. Shorten response times for RFP/RFI and client opportunities.
7. Create a learning loop from Won/Lost opportunities and, later, from estimated-vs-actual delivery data.

## 4. Target users

- Sales / Account teams.
- Pre-sales teams.
- Solution Architects.
- Software Architects.
- Data Architects.
- Cloud Architects.
- DevOps / DevSecOps Architects.
- Pricing / Commercial specialists.
- Proposal / Bid teams.
- Delivery leaders involved in handoff after Won.

## 5. Core experience

The primary experience is conversational.

A user can start with either:

### A. Conversational opportunity

```text
"I have an opportunity to modernize a data platform for a bank..."
```

The system progressively asks for missing information and builds the Deal Spec.

### B. RFP / RFI upload

The user uploads a document. The system:

1. parses the document;
2. extracts requirements;
3. classifies requirements;
4. identifies ambiguities, gaps and contradictions;
5. creates clarification questions;
6. creates or updates the Deal Spec;
7. preserves traceability back to the original document;
8. activates the specialist agents required for the next stage.

> **When an RFP exists, the RFP initiates the Deal Spec. When no RFP exists, the conversation builds it.**

## 6. Agentic operating model

### 6.1 Deal Orchestrator

The main conversational agent. It owns the opportunity state, decides which specialist capability should act next, manages dependencies, asks the user for missing information and coordinates human approval.

### 6.2 Opportunity / Intake Agent

Understands the opportunity or RFP and structures business and technical context.

Expected outputs include:

- objectives;
- scope;
- requirements;
- constraints;
- assumptions;
- exclusions;
- integrations;
- volumetry;
- SLA / RTO / RPO when relevant;
- timeline;
- deliverables;
- clarification questions;
- known / unknown / assumed information.

### 6.3 Precedent / Knowledge Agent

Retrieves comparable historical proposals, solution patterns, reference designs, assumptions, WBS, effort ranges, lessons learned and related evidence.

Initial retrieval can combine:

- metadata filters;
- keyword search;
- vector / semantic search.

The architecture must remain open to future relationship-aware retrieval / knowledge graph / GraphRAG when justified by evidence.

### 6.4 Architect Agent

Proposes technical solution options using three explicit inputs:

```text
Current requirements
      +
Governed architecture knowledge / policies / patterns
      +
Relevant historical precedents
      ↓
Traceable architecture decision
```

The Architect Agent must:

- ask questions when information is insufficient;
- compare alternatives where material;
- identify trade-offs;
- reference the policies, patterns, requirements and precedents used;
- document assumptions;
- generate Architecture Decision Records or equivalent decision evidence;
- never present an unsupported architectural claim as authoritative.

Architecture knowledge can be curated by Solution Architects, Data Architects, Software Architects, Cloud Architects and DevOps/DevSecOps specialists inside the platform.

### 6.5 Effort Estimator Agent

Builds the activity/WBS and estimates roles, FTEs, hours, duration, dependencies and uncertainty.

Historical effort is evidence, not an automatic answer. The agent must explain what precedent or estimation rule was used and which current-deal factors change the estimate.

### 6.6 Pricing Capability / Pricing Agent

Transforms approved effort into cost and client price according to the applicable business-unit rules.

Potential inputs:

- role / band;
- geography;
- business unit;
- rate card;
- currency;
- margin rules;
- discounts;
- contingency;
- tax or commercial rules where applicable.

**Principle:** LLMs may explain pricing, but calculations must be executed through deterministic rules/tools.

### 6.7 Validator Agent

Acts as an independent quality and consistency gate across the lifecycle.

Validation dimensions may include:

- completeness;
- architecture compliance;
- source traceability;
- estimation traceability;
- pricing-rule compliance;
- consistency across artifacts;
- unsupported assumptions;
- unresolved requirements;
- proposal readiness.

### 6.8 Artifact Agent

Generates proposal outputs from the approved Deal Spec instead of reconstructing content independently.

Candidate artifacts:

- technical proposal;
- commercial proposal;
- pricing summary;
- executive presentation;
- statement of work;
- PCR or equivalent handoff artifact;
- compliance matrix;
- WBS;
- assumptions / exclusions;
- risk register;
- client email / response package.

## 7. Deal Spec — single source of truth

The platform uses a structured **Deal Spec** as the canonical state of an opportunity.

```text
Deal
├── Opportunity
├── Client Context
├── Requirements
├── Clarifications
├── Scope
├── Architecture
├── Architecture Decisions
├── Components
├── Precedents
├── WBS
├── Roles / FTE
├── Effort
├── Costs
├── Price
├── Risks
├── Assumptions
├── Exclusions
├── Deliverables
├── Evidence / Sources
├── Validation Results
└── Approvals
```

Generated PPT, proposal, SoW, pricing document or PCR are views derived from this governed source of truth.

## 8. Knowledge model

The solution distinguishes at least four knowledge classes:

| Knowledge class | Examples | Intended use |
|---|---|---|
| Reusable knowledge | patterns, policies, reference architectures, controls | guide decisions |
| Historical evidence | previous proposals, WBS, estimates, lessons learned | compare / support |
| Current master data | rate cards, commercial rules, role catalog | deterministic calculation |
| Opportunity context | client requirements, RFP, constraints, clarifications | parameterize current deal |

Every relevant reusable asset should progressively include metadata such as owner, source, version, effective date, lifecycle status, domain and approval status.

## 9. Human-in-the-loop principles

The platform assists; accountable people approve.

Human approval is required before high-impact transitions such as:

- accepting a final architecture;
- approving commercial assumptions;
- approving effort / staffing baseline;
- releasing external pricing;
- issuing a final proposal;
- promoting an opportunity to delivery handoff.

## 10. Product principles

1. **Do not invent — ask.**
2. **Do not decide without evidence — reference.**
3. **Reuse before rebuilding.**
4. **Separate reasoning from deterministic calculation.**
5. **One Deal Spec, many artifacts.**
6. **Human accountability remains explicit.**
7. **Every Won/Lost result can enrich future decisions.**
8. **Architecture and rigor grow with risk and maturity.**

## 11. Development approach

This repository follows **PA-SDD — Progressive Agentic Spec-Driven Development** from `JuliusCordova/DevPattern`.

For this project:

```text
IDEA
  ↓
FAST DEMO   ← current target
  ↓
MVP
  ↓
PRODUCT
```

The FAST DEMO should prove agentic behavior, traceability and business value with the fewest moving parts. It should not prematurely reproduce the full production architecture.

See:

- `docs/SPEC.md`
- `docs/ARCHITECTURE.md`
- `docs/AGENT_CONTRACTS.md`
- `docs/ROADMAP.md`

## 12. Demo target — Google Cloud

The initial demonstration is planned on GCP using the DevPattern GCP reference baseline.

Initial target components:

- Cloud Run;
- Google ADK;
- Vertex AI / Gemini;
- simple governed tools;
- lightweight persistent state only where needed;
- document / knowledge ingestion required by the demo;
- logging and basic evaluation evidence.

Although the business model is multi-agent, the FAST DEMO should keep deployment/runtime boundaries simple. Specialist agents may initially execute within one controlled ADK application/runtime and only be separated when scale, security, ownership or operational evidence justifies it.

## 13. Initial demo success definition

A demo is successful when a user can:

1. create an opportunity conversationally **or upload an RFP**;
2. obtain structured requirements with source traceability;
3. retrieve relevant precedents;
4. receive a proposed architecture with cited rationale and explicit unknowns;
5. obtain a traceable effort estimate;
6. execute a deterministic demo pricing calculation;
7. run an independent validation step;
8. generate at least one proposal artifact from the same Deal Spec;
9. inspect the evidence used for the important decisions.

## 14. Current status

**Status: Product definition / FAST DEMO specification**

No production-readiness claim is made at this stage.
