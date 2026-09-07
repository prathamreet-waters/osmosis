<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>

# Osmosis

**Osmosis** is an AI-assisted engineering intelligence system that keeps technical knowledge aligned with rapidly changing systems. It detects when engineering changes—code updates, API modifications, configuration shifts, or releases—make existing documentation outdated, and proposes evidence-backed corrections.

The repository contains Product Requirements Documents representing the evolution of Osmosis:

- **[DE: Osmosis Document Engineer - PRD](./documents/prd-de/osmosis-prd-de.md)** — **The final, focused direction:** Keeps engineering documentation synchronized with systems through change detection and evidence-backed update proposals.
- **[S1: Osmosis - Analysis and Engineering Loop - PRD](./documents/prd-s1/osmosis-prd-s1.md)** — Defect analysis using AI evaluation and learning loops for Digital Commerce.
- **[G1: Osmosis - Knowledge and Engineering Loop - PRD](./documents/prd-g1/osmosis-prd-g1.md)** — Original broader enterprise AI and knowledge-platform vision.

**Document Engineer (DE) is the current product direction.** S1 and G1 provide earlier strategic iterations and context.

## The Core Problem

Engineering systems change faster than their documentation.

When developers update code, APIs, configuration, deployment processes, or service behavior, related documentation—READMEs, runbooks, API guides, deployment instructions—often becomes outdated. Over time, this creates documentation drift that erodes trust, increases onboarding friction, and increases dependency on tribal knowledge.

**The root issue:** There is no reliable connection between the *engineering change* and the *documentation that describes that change.*

## Product Promise

Osmosis Document Engineer connects a **specific engineering change** to the **specific documentation affected by that change**, and proposes a focused, evidence-backed correction.

The system:

- **Detects drift early** — Identifies documentation mismatches soon after the source change occurs
- **Connects changes to the right documents** — Avoids manual searches for every potentially affected page
- **Explains rather than merely generates** — Shows why each update is required and where the evidence came from
- **Keeps humans in control** — No change is published without explicit review and approval
- **Prefers precision over volume** — A small number of useful suggestions is more valuable than noise
- **Improves through feedback** — Uses explicit reviewer decisions to enhance future detection

## How It Works

```
1. An engineering change occurs (PR merge, release, API update, config change)
   ↓
2. Osmosis understands what changed
   ↓
3. Osmosis finds related documentation
   ↓
4. Osmosis detects if the documentation is actually affected
   ↓
5. If impacted, Osmosis identifies the mismatch with supporting evidence
   ↓
6. Osmosis creates a focused update proposal
   ↓
7. Document owner reviews and decides: Accept, Edit, Reject, or Mark Irrelevant
   ↓
8. Osmosis publishes only after approval
   ↓
9. Review decisions improve future detection
```

## Evidence-Backed Proposals

Every Osmosis proposal clearly communicates:

- **What changed** — Concise description of the engineering change
- **Which document is affected** — Specific document and relevant section
- **Why it's outdated** — The detected mismatch with context
- **Evidence** — Pull request, commit, configuration, or code reference
- **Suggested correction** — Focused proposed edit
- **Confidence level** — Osmosis's confidence in the recommendation

### Example: Configuration Update

A pull request changes payment timeout from 30 to 60 seconds. The deployment runbook still describes 30 seconds.

Osmosis proposes:

> **What changed:** Payment timeout increased from 30 to 60 seconds (PR #482)  
> **Affected document:** Deployment Runbook  
> **Detected mismatch:** "The payment timeout is 30 seconds"  
> **Suggested correction:** "The payment timeout is 60 seconds"  
> **Evidence:** [Link to PR #482]  
> **Confidence:** High

The document owner can accept, edit, reject, or mark as irrelevant.

## Initial Focus Areas

- eProcurement
- Kerberos
- Customer Onboarding

## MVP Scope

The first version supports:

- One GitHub repository
- README and selected Confluence pages
- Merged pull requests as the change trigger
- Documentation relationship mapping
- Impact detection and mismatch identification
- Evidence-backed draft generation
- Human review and approval workflow
- Publication or documentation pull-request creation
- Basic evaluation metrics

This scope is intentionally narrow—small enough to complete while demonstrating the full product loop from engineering change to approved documentation update.


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>


## DE: Document Engineer – Current Direction

**Osmosis Document Engineer** is the focused, validated direction: keeping engineering documentation aligned with systems through change detection and evidence-backed update proposals.

**Read the Document Engineer PRD:** [documents/prd-de/osmosis-prd-de.md](./documents/prd-de/osmosis-prd-de.md)

### Key Capabilities

- **Change understanding** — Understand meaningful effects of code, configuration, API, release, or process changes
- **Documentation mapping** — Maintain relationships between engineering areas and their documentation
- **Impact analysis** — Determine whether a change actually requires a documentation update
- **Mismatch detection** — Locate exact statements or instructions now incorrect
- **Update generation** — Create focused, grounded proposed edits
- **Evidence presentation** — Show sufficient context for owner review and verification
- **Human review** — Allow owners to accept, modify, reject, or mark proposals
- **Controlled publication** — Publish only after approval
- **Continuous evaluation** — Measure quality and improve from explicit feedback


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>


## S1: Defect Analysis (Previous Direction)

The S1 version focused on defect analysis—helping engineers identify root causes faster using evidence-backed investigation.

### S1 Objective

Help engineers begin defect investigation faster by connecting reported issues with relevant engineering evidence and previously confirmed solutions.

### S1 Solution

When a defect is raised, Osmosis collects authorized context and produces an evidence-backed analysis including:

- Clear problem summary and affected system area
- Similar historical defects with confirmed solutions
- Potentially related pull requests and system changes
- Ranked root-cause hypotheses backed by evidence
- Recommended investigation and resolution steps
- Suggested validation and regression tests
- Confidence levels, missing evidence, and known limitations

The **AI Evaluation Harness** ensured quality and grounding. The **Looping Engineering Engine** used validated outcomes to improve future analysis.

**Read the S1 PRD:** [documents/prd-s1/osmosis-prd-s1.md](./documents/prd-s1/osmosis-prd-s1.md)


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>


## G1: Original Vision (Strategic Context)

The G1 version represents the original Osmosis concept as a secure enterprise AI and knowledge platform serving multiple organizational functions.

### G1 Objective

Provide a governed intelligence layer across internal repositories and enterprise systems, enabling employees to securely discover and use organizational knowledge.

### G1 Platform Capabilities

The original concept included:

- Secure access to enterprise knowledge
- Permission-aware retrieval and cited responses
- Internal and external AI model routing
- Ticket intelligence and prioritization
- Cross-department knowledge discovery
- Continuous AI assistance
- Centralized governance, security, and auditing

G1 established the long-term vision but addressed multiple problems simultaneously. DE was created to validate core value through a focused, measurable problem: keeping documentation aligned with systems.

**Read the G1 PRD:** [documents/prd-g1/osmosis-prd-g1.md](./documents/prd-g1/osmosis-prd-g1.md)


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>
