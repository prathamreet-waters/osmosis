Osmosis Document Engineer

Status: Draft
 Project type: Developer productivity and knowledge automation
 Initial scope: GitHub repositories and Confluence
 Future scope: SharePoint, API documentation, runbooks, and release notes

1. Product Summary

AI-assisted Document Engineer that keeps engineering documentation synchronized with the systems it describes.

It listens to engineering events such as merged pull requests, releases, API contract changes, and configuration updates. It analyzes the change, identifies affected GitHub READMEs, Confluence pages, SharePoint documents, and operational runbooks, then generates an evidence-backed update.

Each proposal includes the detected mismatch, its source, the suggested correction, and a confidence score. Document owners can review, edit, approve, or reject the update before publication. Reviewer feedback and an evaluation harness continuously improve impact detection and draft accuracy.

2. Problem

Engineering documentation becomes outdated because code and systems change faster than developers update:

README files
Confluence pages
SharePoint documents
API documentation
Deployment guides
Operational runbooks

This creates incorrect setup instructions, broken commands, missing configuration details, and unreliable knowledge.

3. Proposed Solution

When an engineering change happens, the system will:

Understand what changed.
Find documentation connected to that change.
Check whether the documentation is now outdated.
Explain the mismatch with evidence.
Draft the required update.
send it to the owner for review.
Publish only after approval.
Use accepted and rejected suggestions to improve future results.
4. Initial User Scenario

A pull request changes:

PAYMENT_TIMEOUT=30


to:

PAYMENT_TIMEOUT=60


The deployment runbook still says the timeout is 30 seconds.

Osmosis detects the mismatch and creates a proposal:

The payment timeout changed from 30 to 60 seconds in PR #482.
 The deployment runbook still uses the previous value.
 Suggested update: replace 30 seconds with 60 seconds.

The document owner can accept, edit, or reject it.

5. How It Knows Something Changed

The system does not repeatedly read everything.

It listens to events from engineering tools:

GitHub PR merged
    ↓
GitHub webhook sends an event
    ↓
Osmosis reads the changed files and PR description
    ↓
It finds documentation related to those files
    ↓
It checks whether the documentation is affected
    ↓
It creates an update proposal


Other triggers can include:

A pull request being merged
A new software release
An API contract changing
A configuration file changing
A service being renamed
A deployment process changing
A GitHub issue being resolved
6. Where the Project Sits

Osmosis sits as an independent service between source systems and documentation systems:

GitHub / CI / Deployment Systems
                ↓
       Change Event Collector
                ↓
       Document Impact Engine
                ↓
      Evidence and Draft Generator
                ↓
       Human Review and Approval
                ↓
Confluence / GitHub README / SharePoint


It is not part of GitHub, Confluence, or SharePoint.

It is a small platform service connected to them through:

GitHub webhooks and APIs
Confluence APIs
SharePoint or Microsoft Graph APIs
Enterprise identity and permissions
7. Core Components
Change Listener

Receives events when code, configuration, APIs, or releases change.

Documentation Map

Maintains relationships such as:

payment-service/
    → Payment Service README
    → Payment API Confluence page
    → Payment deployment runbook


This tells the system which documents may be affected.

Impact Analyzer

Determines whether a change actually requires a documentation update.

It should ignore changes such as formatting, test cleanup, or internal refactoring when they do not affect documented behaviour.

Update Generator

Creates a proposed edit containing:

What changed
Which document is affected
Why it is affected
Supporting PR, commit, or code reference
Suggested document update
Confidence level
Review Workflow

The document owner can:

Accept
Edit and accept
Reject
Mark the suggestion as irrelevant
Evaluation Harness

Measures whether the system:

Found the correct document
Correctly identified outdated content
Avoided unnecessary suggestions
Produced factually grounded updates
Included valid evidence
Improved after reviewer feedback

This keeps the valuable evaluation idea from the earlier Osmosis work, but applies it to a concrete problem.

8. MVP Scope

The first version should support only:

One GitHub repository
README files and selected Confluence pages
Merged pull requests as the trigger
Documentation impact detection
Draft update generation
Human approval
Basic evaluation results

This is narrow enough to finish and strong enough to demonstrate.

9. MVP Demo
Show an accurate README or Confluence page.
Merge a pull request that changes an API or configuration.
Show that the document is now outdated.
Osmosis detects the affected section.
It generates an evidence-backed update.
A developer approves it.
Osmosis updates the document or raises a documentation PR.
10. Success Measures

The MVP succeeds if it can demonstrate:

High accuracy in identifying affected documents
Low unnecessary-update rate
Reduced time spent finding documentation to update
Evidence attached to every proposed change
No automatic publishing without approval
Reviewer acceptance of useful suggestions
11. Out of Scope

The first version will not:

Rewrite the complete company knowledge base
Publish changes without human approval
Treat AI-generated text as fact
Replace Confluence, SharePoint, or GitHub
Access documentation outside the user’s permissions
Continuously crawl every company system
Learn silently from private reviewer behaviour
12. Product Positioning

Osmosis Document Engineer keeps engineering documentation aligned with the systems it describes. It detects when a code or configuration change makes documentation outdated, drafts an evidence-backed correction, and sends it to the responsible person for approval.

The project’s unique value is not AI writing. It is connecting a specific engineering change to the specific documentation that change affects.
