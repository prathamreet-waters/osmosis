# Osmosis Document Engineer

> **Status:** Draft  
> **Project type:** Developer productivity and knowledge automation  
> **Initial scope:** GitHub repositories and Confluence  
> **Future scope:** SharePoint, API documentation, runbooks, and release notes

---

## 1. Product Summary

**Osmosis Document Engineer** is an AI-assisted document engineer that keeps engineering documentation synchronized with the systems it describes.

It listens for meaningful engineering events such as merged pull requests, releases, API contract changes, and configuration updates. It analyzes what changed, identifies the documentation that may be affected, checks whether that documentation is now outdated, and generates an evidence-backed update proposal.

Every proposal clearly communicates:

- What changed
- Which document is affected
- Why the existing content may now be outdated
- The source evidence behind the finding
- The suggested correction
- A confidence level

Document owners remain in control. They can review, edit, approve, reject, or mark a suggestion as irrelevant before anything is published. Reviewer decisions and an evaluation harness help improve impact detection and draft quality over time.

The product's unique value is not simply AI-generated writing. It is the ability to connect a **specific engineering change** to the **specific documentation affected by that change**.

---

## 2. Problem

Engineering systems change faster than their documentation.

When developers update code, configuration, APIs, deployment processes, or service behavior, the related documentation is often not updated at the same time. Over time, this creates documentation drift across:

- README files
- Confluence pages
- SharePoint documents
- API documentation
- Deployment guides
- Operational runbooks
- Release notes

Documentation drift leads to:

- Incorrect setup instructions
- Broken or outdated commands
- Missing configuration details
- Incorrect API behavior descriptions
- Unreliable deployment procedures
- Wasted time validating whether documentation can be trusted
- Increased dependency on tribal knowledge

The core problem is not a lack of documentation. It is the lack of a reliable connection between **system changes** and the **knowledge that describes those systems**.

---

## 3. Product Goal

Keep engineering documentation aligned with the systems it describes by detecting when a meaningful change makes existing documentation outdated and proposing a focused, evidence-backed correction for human approval.

### Product principles

1. **Detect drift early**  
   Identify documentation mismatches soon after the source change occurs.

2. **Connect changes to the right documents**  
   Avoid forcing people to manually search for every page or guide that may be affected.

3. **Explain rather than merely generate**  
   Every suggestion must show why the update is required and where the evidence came from.

4. **Keep humans in control**  
   No proposed change is published without explicit review and approval.

5. **Prefer precision over volume**  
   A small number of useful suggestions is more valuable than many noisy or irrelevant ones.

6. **Improve through explicit feedback**  
   Accepted, edited, rejected, and irrelevant suggestions should improve future results in a transparent and measurable way.

---

## 4. Proposed Solution

When an engineering change occurs, Osmosis will:

1. Understand what changed.
2. Find documentation connected to that change.
3. Determine whether the change affects documented behavior or instructions.
4. Ignore changes that do not require documentation updates.
5. Identify and explain any mismatch with supporting evidence.
6. Draft a focused correction.
7. Send the proposal to the responsible document owner.
8. Publish only after approval.
9. Use the review decision to evaluate and improve future suggestions.

### Osmosis operating loop

```mermaid
flowchart LR
    A["1. Something changes"] --> B["2. Understand the change"]
    B --> C["3. Find related documentation"]
    C --> D{"4. Is the documentation<br/>actually affected?"}

    D -->|"No"| E["Ignore the change"]
    D -->|"Yes"| F["5. Identify the mismatch"]
    F --> G["6. Create an evidence-backed update"]
    G --> H["7. Send it to the document owner"]

    H --> I{"8. Owner decides"}
    I -->|"Accept"| J["Publish the correction"]
    I -->|"Edit"| K["Refine and publish"]
    I -->|"Reject"| L["Do not publish"]

    J --> M["9. Learn from the decision"]
    K --> M
    L --> M
    M --> B

    classDef event fill:#FFF4E5,stroke:#D88A20,color:#3B280B,stroke-width:2px
    classDef intelligence fill:#E8F0FE,stroke:#4C78D0,color:#14284A,stroke-width:2px
    classDef decision fill:#FFF8D8,stroke:#C49A17,color:#3F3208,stroke-width:2px
    classDef human fill:#F3E8FF,stroke:#8B5FC7,color:#32184F,stroke-width:2px
    classDef publish fill:#E6F6EC,stroke:#3E9B61,color:#153D24,stroke-width:2px
    classDef stop fill:#FCE8E6,stroke:#C9574D,color:#4D1713,stroke-width:2px

    class A event
    class B,C,F,G,M intelligence
    class D,I decision
    class H human
    class J,K publish
    class E,L stop
```

---

## 5. Initial User Scenario

A pull request changes the payment timeout configuration from:

```text
PAYMENT_TIMEOUT=30
```

to:

```text
PAYMENT_TIMEOUT=60
```

However, the deployment runbook still states that the payment timeout is 30 seconds.

Osmosis detects the mismatch and creates a proposal:

> The payment timeout changed from 30 to 60 seconds in PR #482. The deployment runbook still uses the previous value. Suggested update: replace 30 seconds with 60 seconds.

The document owner can accept the proposal, edit it before accepting, reject it, or mark it as irrelevant.

### Example experience

```mermaid
sequenceDiagram
    participant Change as Engineering Change
    participant Osmosis
    participant Doc as Deployment Runbook
    participant Owner as Document Owner

    Note over Change: Payment timeout changes<br/>from 30 to 60 seconds
    Change->>Osmosis: Change completed

    Osmosis->>Doc: Check related instructions
    Doc-->>Osmosis: Runbook still says 30 seconds

    Note over Osmosis: Mismatch detected

    Osmosis->>Owner: Propose replacing<br/>30 seconds with 60 seconds
    Note over Owner: Proposal includes the change,<br/>affected instruction, evidence,<br/>and suggested correction

    alt Owner accepts
        Owner->>Doc: Approve correction
        Note over Doc: Runbook now says 60 seconds
    else Owner edits
        Owner->>Doc: Refine and approve correction
    else Owner rejects
        Owner-->>Osmosis: Do not update
    end
```

---

## 6. How Osmosis Knows Something Changed

Osmosis does not repeatedly read or crawl every connected system. It responds to meaningful events generated by engineering workflows.

For example:

1. A pull request is merged.
2. Osmosis receives the change event.
3. It reads the changed files and the context describing the change.
4. It identifies documentation connected to the affected area.
5. It checks whether the documentation is meaningfully impacted.
6. It creates an update proposal when a mismatch is found.

Potential triggers include:

- A pull request being merged
- A new software release
- An API contract changing
- A configuration value changing
- A service being renamed
- A deployment process changing
- A GitHub issue being resolved

The system should focus on meaningful behavioral or operational changes. Formatting updates, test cleanup, comments, and internal refactoring should be ignored when they do not change anything users need to understand or do.

---

## 7. Documentation Relationships

Osmosis needs to understand which documents describe which parts of an engineering system.

For example:

```text
payment-service/
    -> Payment Service README
    -> Payment API Confluence page
    -> Payment deployment runbook
```

These relationships help Osmosis narrow its search and determine which documents are reasonable candidates for impact analysis.

A relationship may be established through explicit ownership, links, repository structure, references, historical updates, or other reliable signals. The MVP should prefer clear and controlled relationships over attempting to understand an entire company knowledge base.

---

## 8. Evidence-Backed Update Proposal

An Osmosis proposal must be understandable and reviewable without asking the document owner to repeat the investigation.

Each proposal should include:

- **What changed:** A concise description of the engineering change
- **Affected document:** The specific document and relevant section
- **Detected mismatch:** The content that may now be outdated
- **Reason:** Why the engineering change affects that content
- **Evidence:** The supporting pull request, commit, configuration, or code reference
- **Suggested correction:** A focused proposed edit
- **Confidence level:** Osmosis's confidence that the document requires this update

### What the document owner sees

```mermaid
flowchart TB
    A["Osmosis Update Proposal"]

    A --> B["What changed"]
    A --> C["Which document is affected"]
    A --> D["Why the document is now outdated"]
    A --> E["Evidence from the source change"]
    A --> F["Suggested correction"]
    A --> G["Confidence level"]

    B --> H["A complete, reviewable explanation"]
    C --> H
    D --> H
    E --> H
    F --> H
    G --> H

    H --> I{"Document owner's decision"}

    I -->|"Accept"| J["Publish as proposed"]
    I -->|"Edit and accept"| K["Publish the refined version"]
    I -->|"Reject"| L["Leave the document unchanged"]
    I -->|"Irrelevant"| M["Improve future detection"]

    classDef proposal fill:#E8F0FE,stroke:#4C78D0,color:#14284A,stroke-width:2px
    classDef evidence fill:#F5F7FA,stroke:#7A8796,color:#202A35,stroke-width:1.5px
    classDef trust fill:#FFF8D8,stroke:#C49A17,color:#3F3208,stroke-width:2px
    classDef decision fill:#F3E8FF,stroke:#8B5FC7,color:#32184F,stroke-width:2px
    classDef positive fill:#E6F6EC,stroke:#3E9B61,color:#153D24,stroke-width:2px
    classDef negative fill:#FCE8E6,stroke:#C9574D,color:#4D1713,stroke-width:2px

    class A proposal
    class B,C,D,E,F,G evidence
    class H trust
    class I decision
    class J,K positive
    class L,M negative
```

---

## 9. Review and Approval Workflow

The document owner can:

- **Accept:** Publish the correction as proposed
- **Edit and accept:** Refine the wording before publication
- **Reject:** Decline the proposed update
- **Mark as irrelevant:** Indicate that the detected relationship or impact was not useful

No document should be changed automatically in the initial product experience. Human approval is a core product requirement, not merely a temporary safeguard.

Reviewer feedback must be used carefully and transparently. Osmosis should learn from explicit decisions, but it must not silently infer preferences from private reviewer behavior.

---

## 10. Evaluation Harness

The evaluation harness determines whether Osmosis is producing useful, grounded, and appropriately targeted suggestions.

It should measure whether the system:

- Found the correct document
- Identified the correct section
- Correctly recognized outdated content
- Ignored changes that did not require documentation updates
- Avoided unnecessary suggestions
- Produced a factually grounded correction
- Included valid and sufficient evidence
- Improved after explicit reviewer feedback

The purpose of evaluation is not simply to measure writing quality. It is to verify the complete chain from change detection to document selection, mismatch identification, evidence quality, and reviewer usefulness.

---

## 11. Core Product Capabilities

### 11.1 Change understanding

Understand the meaningful effect of a code, configuration, API, release, or process change.

### 11.2 Documentation mapping

Maintain relationships between engineering areas and the documentation that describes them.

### 11.3 Impact analysis

Determine whether an engineering change actually requires a documentation update.

### 11.4 Mismatch detection

Locate the exact statement, instruction, command, value, or section that may now be incorrect.

### 11.5 Update generation

Create a focused proposed edit grounded in the source change.

### 11.6 Evidence presentation

Show enough supporting context for the owner to understand and verify the proposal.

### 11.7 Human review

Allow the responsible owner to accept, modify, reject, or mark a proposal as irrelevant.

### 11.8 Controlled publication

Publish only after approval, either by updating the selected document or by raising a documentation change for review.

### 11.9 Continuous evaluation

Measure quality and use explicit review outcomes to improve future detection and drafting.

---

## 12. MVP Scope

The first version should support only:

- One GitHub repository
- README files and selected Confluence pages
- Merged pull requests as the trigger
- Documentation relationship mapping
- Documentation impact detection
- Mismatch identification
- Evidence-backed draft generation
- Human review and approval
- Basic publication or documentation pull-request creation
- Basic evaluation results

This scope is intentionally narrow. It is small enough to complete while still demonstrating the full product loop from engineering change to approved documentation correction.

---

## 13. MVP Demo

The MVP demonstration should tell one simple, complete story:

1. Show an accurate README or Confluence page.
2. Merge a pull request that changes an API, configuration, or documented behavior.
3. Show that the existing document is now outdated.
4. Show Osmosis identifying the affected document and section.
5. Show the detected mismatch and supporting evidence.
6. Show the proposed correction and confidence level.
7. Have a developer review and approve the proposal.
8. Show Osmosis updating the document or raising a documentation pull request.
9. Show the review result reflected in the evaluation output.

The demo should prioritize correctness and clarity over breadth. One convincing end-to-end example is more valuable than multiple incomplete cases.

---

## 14. Success Measures

The MVP succeeds if it demonstrates:

- High accuracy in identifying affected documents
- High accuracy in locating the affected section
- Low unnecessary-update rate
- Reduced time spent finding documentation that needs updating
- Evidence attached to every proposed change
- Factually grounded suggested corrections
- No automatic publication without approval
- Strong reviewer acceptance of useful suggestions
- Clear handling of rejected and irrelevant suggestions

The most important signal is whether reviewers consistently consider the proposals useful and trustworthy.

---

## 15. Out of Scope

The first version will not:

- Rewrite the complete company knowledge base
- Publish changes without human approval
- Treat AI-generated text as fact
- Replace Confluence, SharePoint, GitHub, or other documentation systems
- Access documentation outside the user's permissions
- Continuously crawl every company system
- Learn silently from private reviewer behavior
- Support every repository and document source from day one
- Attempt large-scale style rewriting unrelated to a detected engineering change

---

## 16. Product Promise and Boundaries

```mermaid
mindmap
  root((Osmosis<br/>Document Engineer))
    Keeps knowledge aligned
      Detects documentation drift
      Connects changes to affected documents
      Suggests focused corrections
      Restores documentation trust
    Builds confidence
      Explains every mismatch
      Includes supporting evidence
      Shows confidence level
      Keeps the owner in control
    Protects quality
      Ignores irrelevant changes
      Measures unnecessary suggestions
      Uses reviewer feedback
      Evaluates factual grounding
    Will not
      Publish without approval
      Treat generated text as fact
      Replace documentation platforms
      Access unauthorized content
      Rewrite the entire knowledge base
```

---

## 17. Risks and Guardrails

### Incorrect document relationships

Osmosis may associate a change with the wrong document.

**Guardrail:** Use confidence levels, explicit mappings where possible, clear evidence, and an “irrelevant” review option.

### Excessive or noisy suggestions

Too many low-value proposals could cause reviewers to ignore the product.

**Guardrail:** Prefer precision over recall in the MVP and measure the unnecessary-update rate.

### Unsupported or invented corrections

A generated draft may include claims not supported by the source change.

**Guardrail:** Require evidence for every proposal, constrain corrections to the detected mismatch, and keep a human approval step.

### Unauthorized access

Connected documentation may contain information a user is not permitted to view or modify.

**Guardrail:** Respect existing user identity, ownership, and document permissions throughout detection, review, and publication.

### Overreliance on automation

Users may begin to treat generated proposals as automatically correct.

**Guardrail:** Present Osmosis as a document engineering assistant, clearly expose confidence and evidence, and never treat generated text as fact.

---

## 18. Future Scope

After the MVP proves the core change-to-document connection, Osmosis may expand to:

- Additional GitHub repositories
- SharePoint documents
- API documentation
- Operational runbooks
- Deployment guides
- Release notes
- Additional engineering change events
- Broader documentation relationship discovery
- More advanced evaluation and reporting

Expansion should preserve the same core principles: focused impact detection, evidence-backed proposals, permission-aware access, and human-controlled publication.

---

## 19. Product Positioning

**Osmosis Document Engineer keeps engineering documentation aligned with the systems it describes. It detects when a code, configuration, API, release, or process change makes documentation outdated, drafts an evidence-backed correction, and sends it to the responsible person for approval.**

Osmosis is not another AI writing tool. Its central value is the connection between a real engineering change and the exact documentation that change affects.

---

## 20. One-Line Product Story

> **Change happens. Knowledge drifts. Osmosis finds the connection, explains the mismatch, and helps the owner restore trust.**
