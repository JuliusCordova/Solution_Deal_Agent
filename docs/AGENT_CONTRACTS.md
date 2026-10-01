# Agent Contracts — Solution Deal Agent

Status: CONSTRUCTION BASELINE  
Mode: FAST DEMO

## 1. Contract principles

Every agent has a clear responsibility, explicit inputs/outputs, permitted tools, evidence expectations, escalation rules and uncertainty behavior.

Global rules:

- agents must not silently fabricate missing business information;
- specialist agents do not own canonical state directly; they use Deal Spec services;
- source documents must enter knowledge processing through controlled GCS input;
- critical business rules remain outside free-form prompts;
- every material architecture/commercial claim should expose evidence or state insufficient evidence.

## 2. Deal Orchestrator

### Purpose
Coordinate conversation and deal lifecycle.

### Inputs
- user intent;
- Deal Spec;
- lifecycle state;
- validation state;
- specialist/tool results.

### Outputs
- next action;
- delegated task;
- clarification question;
- lifecycle transition proposal;
- progress summary.

### Rules
- never bypass approval gates;
- preserve one canonical Deal Spec;
- delegate specialist reasoning;
- surface critical unknowns;
- do not permit clean proposal-ready state with unresolved blocking findings.

## 3. Intake / RFP Agent

### Purpose
Transform opportunity information and RFP/source documents into structured deal requirements.

### Inputs
- conversation;
- GCS-backed source document references;
- supporting documents;
- current Deal Spec;
- GraphRAG evidence when needed.

### Outputs
- structured requirements;
- classifications;
- source references;
- known/unknown/assumed/derived status;
- clarification questions;
- client constraints and deliverables.

### Rules
- uploaded files must be persisted to GCS input before analysis;
- preserve source GCS URI/version and locator;
- distinguish facts from assumptions;
- do not promote ambiguous text to confirmed requirement without evidence.

## 4. Knowledge / GraphRAG Agent

### Purpose
Retrieve governed architecture knowledge and comparable precedents using hybrid semantic + graph retrieval.

### Inputs
- Deal Spec search context;
- task/domain;
- metadata filters;
- optional entity seeds.

### Outputs
- ranked evidence packet;
- source/chunk references;
- graph relationships/path used;
- relevance/confidence notes;
- insufficient-evidence result when appropriate.

### Allowed tools/services
- `knowledge.search_vector`
- `knowledge.traverse_graph`
- `knowledge.search_hybrid`
- `document.get_source_fragment`

### Rules
- architecture knowledge and historical precedents remain separately identifiable;
- historical price is not current authoritative price;
- evidence must preserve source identity;
- graph traversal is bounded;
- unsupported retrieval is not converted into a fact;
- return `INSUFFICIENT_EVIDENCE` when retrieval does not meet the configured threshold.

## 5. Architect Agent

### Purpose
Propose and explain technical solution decisions.

### Inputs
- confirmed/assumed requirements;
- opportunity constraints;
- governed architecture GraphRAG evidence;
- relevant precedent GraphRAG evidence;
- unresolved clarifications.

### Outputs
- proposed architecture;
- ADR-like architecture decisions;
- alternatives/trade-offs where material;
- assumptions;
- remaining questions;
- evidence references.

### Rules
- do not close a material decision when a critical unknown makes it misleading;
- cite requirements behind material decisions;
- prefer approved/current policies and patterns;
- treat historical proposals as precedent, not policy;
- explicitly record exceptions;
- separate facts, recommendations and assumptions.

## 6. Effort Estimator Agent

### Purpose
Convert approved scope/design into a transparent effort model.

### Inputs
- Deal Spec scope;
- selected architecture/components;
- WBS templates/rules;
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
- identify high-uncertainty lines;
- do not calculate authoritative client price.

## 7. Pricing Capability

### Purpose
Calculate reproducible cost/client price from approved structured inputs.

### Inputs
- effort by role/band;
- business-unit rules;
- rate card;
- currency;
- margin/discount/contingency rules;
- configured taxes/fees where relevant.

### Outputs
- cost;
- price;
- margin;
- calculation breakdown;
- rule/rate-card version;
- input snapshot.

### Rules
- deterministic execution;
- LLM cannot override result;
- missing required pricing input produces clarification/error, not an invented value.

## 8. Validator Agent

### Purpose
Independently assess deal readiness and cross-domain consistency.

### Inputs
- Deal Spec;
- architecture decisions;
- evidence packets;
- estimate;
- pricing result;
- generated artifacts;
- validation policies.

### Outputs
- findings;
- severity;
- evidence/reference;
- remediation;
- readiness result.

### Initial validation dimensions
- requirement completeness;
- architecture-policy alignment;
- evidence coverage;
- estimate traceability;
- pricing integrity;
- unresolved assumptions;
- scope/WBS consistency;
- duration consistency;
- artifact consistency;
- source provenance.

### Rules
- independent from artifact drafting;
- blocking findings stop clean readiness;
- accepted exceptions are explicit human decisions.

## 9. Artifact Agent

### Purpose
Generate artifacts from an approved structured Deal Spec.

### Inputs
- Deal Spec version;
- artifact template;
- approved technical/commercial content;
- validation status.

### Outputs
- technical proposal draft;
- economic/pricing summary;
- generation metadata.

### Rules
- cannot invent different scope, duration, price or commitments;
- must use canonical values;
- unsupported narrative claims are cited, flagged or removed;
- artifact generation is not approval.

## 10. Human approval contract

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

## 11. Ingestion / chunking tool contract

```yaml
ingest_document:
  input:
    gcs_uri: gs://solution-deal-agent-demo/input/...
    gcs_generation: string
    knowledge_domain: architecture | precedent | opportunity
  preconditions:
    - object exists
    - URI belongs to approved input location
  output:
    document_id: string
    normalized_artifact: string
    chunk_manifest: string
    chunk_count: integer
    chunker_version: string
```

The chunking capability rejects local paths and arbitrary URLs as authoritative inputs.

## 12. GraphRAG evidence contract

```yaml
evidence_packet:
  query_id: string
  domain: architecture | precedent | opportunity
  items:
    - source_document_id: string
      chunk_id: string
      source_gcs_uri: string
      source_generation: string
      locator: string
      relevance_score: number
      authority_status: string
      graph_path: []
  outcome: EVIDENCE_FOUND | INSUFFICIENT_EVIDENCE
```

## 13. Tool boundary

Agents reason; tools/services perform bounded actions.

Initial tool surface:

- `deal.create`
- `deal.get`
- `deal.update_section`
- `deal.add_requirement`
- `deal.add_architecture_decision`
- `deal.add_estimate`
- `deal.add_validation_finding`
- `document.register_gcs_source`
- `document.ingest_from_gcs`
- `knowledge.search_vector`
- `knowledge.traverse_graph`
- `knowledge.search_hybrid`
- `document.get_source_fragment`
- `pricing.calculate`
- `artifact.generate`
- `approval.record`

Side-effect tools expose explicit schemas and inspectable results.