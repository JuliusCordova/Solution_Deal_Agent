# Agent Contracts — Solution Deal Agent

Status: DRAFT  
Mode: FAST DEMO

## 1. Contract principles

Every agent must have:

- a clear responsibility;
- explicit inputs;
- explicit outputs;
- permitted tools;
- evidence expectations;
- escalation / human-approval rules;
- failure and uncertainty behavior.

Agents must not silently fabricate missing business information.

## 2. Deal Orchestrator

### Purpose
Coordinate the user conversation and deal lifecycle.

### Inputs
- user intent;
- current Deal Spec;
- lifecycle state;
- validation status;
- agent/tool results.

### Outputs
- next action;
- delegated specialist task;
- clarification question;
- lifecycle transition proposal;
- user-facing progress summary.

### Rules
- never bypass required approval gates;
- preserve one canonical Deal Spec;
- delegate specialist analysis instead of duplicating domain reasoning;
- surface unresolved critical unknowns;
- do not allow proposal-ready status while blocking findings remain unresolved unless a human explicitly accepts the exception.

## 3. Intake / RFP Agent

### Purpose
Transform opportunity information and source documents into structured deal requirements.

### Inputs
- user conversation;
- uploaded RFP/RFI;
- optional supporting documents;
- current Deal Spec.

### Outputs
- structured requirements;
- requirement classification;
- source references;
- known / unknown / assumed status;
- clarification questions;
- extracted client constraints and deliverables.

### Rules
- preserve source references;
- distinguish extracted facts from inferred assumptions;
- do not promote ambiguous text to confirmed requirement without evidence;
- request clarification for material gaps.

## 4. Precedent / Knowledge Agent

### Purpose
Find reusable and comparable knowledge relevant to the current opportunity.

### Inputs
- Deal Spec search context;
- requested knowledge domain;
- metadata filters.

### Outputs
- ranked evidence items;
- similarity rationale;
- source metadata;
- confidence/relevance notes.

### Rules
- keep architecture knowledge separate from historical commercial precedent;
- never treat historical price as current authoritative price;
- expose source identity and available metadata;
- return "no sufficient evidence" when appropriate.

## 5. Architect Agent

### Purpose
Propose and explain technical solution decisions.

### Inputs
- confirmed/assumed requirements;
- current opportunity constraints;
- governed architecture knowledge;
- relevant historical precedents;
- unresolved clarifications.

### Outputs
- proposed architecture;
- architecture decisions;
- alternatives where material;
- trade-offs;
- assumptions;
- questions still required;
- evidence references.

### Rules
- do not close a material decision if a critical unknown makes it unsafe or misleading;
- cite current requirements behind major decisions;
- use approved patterns/policies where available;
- use historical proposals as supporting precedent, not policy;
- record exceptions explicitly;
- separate facts, recommendations and assumptions.

## 6. Effort Estimator Agent

### Purpose
Convert approved scope/design into a transparent effort model.

### Inputs
- Deal Spec scope;
- architecture solution;
- WBS templates / rules;
- relevant precedents;
- role catalog;
- assumptions.

### Outputs
- WBS;
- roles;
- FTE/hours;
- duration assumptions;
- dependencies;
- confidence/range;
- estimate rationale.

### Rules
- historical effort is evidence, not a direct copy target;
- explain material adjustment factors;
- keep commercial rate information outside the reasoning unless explicitly needed by pricing;
- identify high-uncertainty line items.

## 7. Pricing Capability

### Purpose
Calculate reproducible cost and client price from approved structured inputs.

### Inputs
- effort by role/band;
- unit/business rule set;
- rate card;
- currency;
- margin/discount/contingency rules;
- configured taxes or fees where relevant.

### Outputs
- cost;
- price;
- margin;
- calculation breakdown;
- rule version / input snapshot.

### Rules
- calculation must be deterministic;
- LLM cannot override calculation result;
- every price must be reproducible from stored inputs and rule version;
- missing required pricing inputs produce an error/clarification, not an invented value.

## 8. Validator Agent

### Purpose
Independently assess deal readiness and cross-domain consistency.

### Inputs
- Deal Spec;
- architecture decisions;
- estimate;
- pricing result;
- generated artifacts;
- policy/validation rules.

### Outputs
- findings;
- severity;
- evidence/reference;
- recommended remediation;
- readiness result.

### Initial validation dimensions
- requirement completeness;
- architecture-policy alignment;
- architecture evidence coverage;
- estimate traceability;
- pricing calculation integrity;
- unresolved assumptions;
- scope/WBS consistency;
- duration consistency;
- artifact consistency;
- source traceability.

### Rules
- validator must be independent from the artifact drafting step;
- blocking findings stop clean proposal-ready status;
- accepted exceptions must be recorded as human decisions.

## 9. Artifact Agent

### Purpose
Generate business artifacts from the approved structured Deal Spec.

### Inputs
- Deal Spec version;
- selected artifact template;
- approved technical/commercial content;
- validation status.

### Outputs
- draft proposal artifact;
- metadata identifying Deal Spec version and generation time.

### Rules
- cannot invent alternative scope, duration, price or commitments;
- must use canonical values;
- unsupported narrative claims should reference evidence or be removed;
- artifact generation does not constitute approval.

## 10. Human approval contract

For FAST DEMO, a human approval record contains:

```yaml
approval:
  deal_id: string
  deal_spec_version: string
  decision: APPROVE | REJECT | APPROVE_WITH_EXCEPTION
  actor: string
  timestamp: datetime
  notes: string
  accepted_findings: []
```

Only an explicit approval may transition the opportunity to `PROPOSAL_READY`.

## 11. Tool boundary

Agents reason; tools perform bounded actions.

Examples:

- retrieve evidence;
- read source fragments;
- mutate structured Deal Spec fields;
- calculate pricing;
- generate a file;
- record approval.

Tools that create side effects must expose explicit schemas and return inspectable results.
