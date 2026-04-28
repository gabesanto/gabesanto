# Building Production AI Agents for Complex B2B Data Workflows

A short, sanitized case study on designing AI agents for production data workflows where accuracy, traceability, and reviewability matter.

## Context

B2B data workflows often involve high variance across sources, formats, confidence levels, and edge cases.

The challenge is not just to automate a task with an LLM. The challenge is to design a reliable product system that can combine deterministic checks, retrieval, AI reasoning, observability, and human review without turning the workflow into a black box.

## What I built

I designed and shipped a production AI-assisted pipeline focused on data hygiene and readiness.

The pipeline supports:

- Data normalization
- Deduplication and conflict resolution
- Cross-checks against existing records and business rules
- Retrieval-augmented checks for additional context
- Completeness and data quality validation
- Confidence-based routing
- Structured outputs for ready, review, and not-ready cases
- Configurable workflow options at run start
- Optional/skippable steps depending on the use case
- Step-level observability for auditability and debugging

## Agent orchestration model

The workflow is designed more like a factory than a single monolithic agent.

A coordinating agent owns the overall process, while specialized sub-agents handle focused steps. Each step has a narrower responsibility, clearer inputs, clearer outputs, and more predictable behavior.

This separation makes the system easier to evaluate, debug, tune, and improve over time.

## Product flexibility

The workflow is not a rigid one-size-fits-all pipeline.

Users can customize which checks should run when starting the workflow. This makes the agent more useful across different operational contexts: some runs need the full pipeline, while others only need a subset of checks.

This matters because production AI systems should adapt to the workflow instead of forcing every user through the same path.

## Design principles

### Deterministic where correctness matters

Rules-based checks handle the parts of the workflow that should be predictable, repeatable, and easy to audit.

### AI where ambiguity exists

LLM reasoning is used only where context and judgment are valuable, especially for cases where rigid rules are too brittle.

### Retrieval before reasoning

The agent should not reason in isolation. It should retrieve relevant existing records, business rules, and workflow context before making or suggesting decisions.

### Specialized agents over a monolith

Each sub-agent should behave like a specialized machine in a factory: focused on one responsibility, easier to test, and easier to improve without destabilizing the whole workflow.

### Review queues over silent automation

Low-confidence or ambiguous outputs should be routed to review instead of being forced through the workflow.

### Configurable by design

Production workflows are rarely identical every time. Agent steps should be configurable, skippable, and explicit so users can adapt the system to the job they are running.

### Evals and observability as product requirements

Production AI agents need measurable outputs, step-by-step traces, and feedback loops. Evals are not a separate research artifact; they are part of the product architecture.

## Architecture themes

- Agentic pipeline design
- Coordinator/sub-agent orchestration
- Specialized agents with narrow responsibilities
- Rails and Python service boundaries
- Background jobs and async processing
- Webhook-based completion flows
- User-configurable run options
- Optional/skippable agent steps
- Structured run metadata and cleanup reports
- Human-in-the-loop review paths
- RAG-style retrieval over existing data and business context
- Product-facing outputs instead of one-off scripts

## Outcome

Early production runs have been very strong.

There is no large public benchmark to share yet, but for the reviewed core scenarios the system was designed around, outputs reached roughly **99% confidence after iteration and tuning**.

The most important result: the workflow became more structured, observable, configurable, and repeatable.

## What this reflects

This is the kind of AI engineering I care about:

Not wrapping an LLM around a workflow and hoping it works.

But decomposing a complex business process into reliable components, adding retrieval and reasoning where they actually help, measuring outputs, and turning the whole thing into a product-grade system.

AI agents become valuable when they stop being magic tricks and start becoming operational leverage.
