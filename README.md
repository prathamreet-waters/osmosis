# Product Requirements Document

Waters AI Vault

**Status:** Draft for product and architecture review

**Product type:** Secure enterprise AI and knowledge platform

**Target environment:** Waters-controlled on-premises or approved hybrid infrastructure

## 1. Product Overview

Waters AI Vault is a centralized, access-controlled AI platform that allows employees to work with internal code, scientific documents, enterprise knowledge, service information, and engineering data.

The platform provides secure AI access while preserving existing user permissions, protecting proprietary information, and preventing sensitive requests from reaching unapproved AI services.

Waters AI Vault is not intended to replace existing repositories, ticketing systems, scientific systems, or decision owners. It operates as an intelligence layer across them.

## 2. Product Vision

Enable Waters employees to securely use AI across engineering, science, service, quality, and business functions while keeping proprietary knowledge governed within Waters-controlled boundaries.

## 3. Problem Statements

### 3.1 Unsafe AI Usage

Employees cannot safely use public AI services with proprietary code, scientific knowledge, regulated content, or enterprise data.

### 3.2 Fragmented Enterprise Knowledge

Critical knowledge is distributed across repositories, documents, tickets, systems, and subject-matter experts, making discovery and reuse difficult.

### 3.3 Unauthorized Information Exposure

AI retrieval may expose information beyond a user’s role, document permissions, or legitimate business need.

### 3.4 Disconnected AI Solutions

Departments build isolated AI tools, duplicating infrastructure, cost, governance, security controls, and operational effort.

### 3.5 Inadequate Model Routing

Requests with different sensitivity, domain, capability, latency, and cost requirements are not consistently routed to the appropriate AI model.

### 3.6 Limited Traceability and Auditability

The organization lacks consistent visibility into AI usage, accessed sources, policy decisions, model selection, and generated outputs.

### 3.7 Slow Research and Troubleshooting

Employees spend significant time locating relevant code, scientific methods, SOPs, service history, and technical knowledge.

### 3.8 Risk in Regulated Workflows

AI-generated output may be treated as approved scientific, quality, safety, or regulatory guidance without sufficient evidence or human review.

### 3.9 Static Cross-Department Ticket Prioritization

Ticket priorities are assigned within individual teams and may not reflect active releases, dependencies, business impact, or enterprise-wide incidents.

### 3.10 Unverified and Outdated Work Items

Teams may invest effort in duplicate, obsolete, incorrectly prioritized, insufficiently validated, or already-resolved tickets.

### 3.11 Excessive Access for Knowledge Discovery

Traditional knowledge sharing often requires direct access to repositories or documents, exposing more information than users need to complete a task.

## 4. Proposed Solutions

### 4.1 Looping Engineering Engine

Continuously evaluates tickets, releases, dependencies, incidents, feedback, and business context.

The engine identifies duplicate, outdated, or incorrectly prioritized work and provides explainable recommendations. Final ownership and approval remain with authorized teams.

### 4.2 AI Evaluation Harness

Validates access controls, retrieval quality, citations, model routing, prompt-injection resistance, model performance, and data-leakage controls.

The harness ensures that changes to models, prompts, policies, or knowledge sources do not silently weaken the platform.

### 4.3 Secure Knowledge Mediation

Allows users to query protected information through permission-aware and cited AI responses without receiving unnecessary access to the underlying repositories or documents.

The platform provides only the information permitted for the user and the specific business task.

### 4.4 Policy-Based AI Router

Selects an internal or approved external model based on:

- Data sensitivity
- User authorization
- Business domain
- Required capability
- Cost
- Latency
- Availability

Sensitive or uncertain requests remain within the Waters-controlled model environment.

### 4.5 Governed Secondary Knowledge Layer

Creates controlled summaries, relationships, classifications, and derived knowledge from approved sources.

This enables cross-department collaboration without exposing unrestricted raw content. Derived knowledge retains its source references, classification, permissions, and ownership.

### 4.6 Continuous AI Assistant

Performs authorized background tasks such as:

- Issue discovery
- Ticket validation
- Duplicate detection
- Feedback analysis
- Dependency monitoring
- Knowledge updates

Continuous tasks operate within defined schedules, permissions, resource limits, and stopping conditions.

## 5. Target Users

### 5.1 Developers and Engineers

- Search and explain approved internal code.
- Analyze dependencies and change impact.
- Find related tickets and technical documentation.
- Generate tests, summaries, and documentation.
- Assess ticket priority against release context.

### 5.2 Laboratory Scientists

- Search approved scientific methods, SOPs, and application notes.
- Compare procedures and historical investigations.
- Retrieve cited troubleshooting knowledge.
- Access approved engineering knowledge through secure AI mediation.

### 5.3 Service and Support Engineers

- Find similar historical incidents.
- Analyze instrument logs and service cases.
- Identify recurring issue patterns.
- Generate diagnostic checklists and cited recommendations.

### 5.4 Quality and Regulatory Teams

- Search approved policies, records, and SOPs.
- Compare documents against approved templates.
- Prepare cited summaries and audit-support material.
- Review evidence without allowing autonomous approval.

### 5.5 Product and Engineering Managers

- Review release dependencies and business impact.
- Identify duplicate or outdated work.
- Receive explainable priority recommendations.
- Accept or reject AI recommendations.

### 5.6 Platform Administrators
 

Register approved models and knowledge sources. 

Configure routing and data-handling policies. 

Manage role-based access. 

Monitor model usage, cost, performance, and audit events. 

Disable models, connectors, or sources centrally. 

 
 

6. Core Product Capabilities 

6.1 Secure AI Interface 

A centralized chat and developer interface for accessing approved internal and external AI models. 

6.2 Enterprise Identity and Access 

Users authenticate using enterprise identity. Existing roles and source permissions determine the knowledge available to each request. 

6.3 Permission-Aware RAG 

The platform retrieves only the documents and knowledge that the authenticated user is authorized to access. 

Authorization must be applied before content reaches the model. 

6.4 Cited Responses 

Knowledge-based responses include references to the supporting sources. 

When sufficient evidence is unavailable, the system should return an insufficient-evidence response rather than presenting an unsupported answer. 

6.5 Ticket Intelligence 

The platform evaluates tickets using: 

Release context 

Dependencies 

Business impact 

Related incidents 

Existing priority 

Ticket age 

Duplicate likelihood 

Supporting evidence 

The output includes a recommended priority, explanation, related items, and citations. 

6.6 Internal and External Model Routing 

Sensitive requests use a Waters-controlled model. 

Approved non-sensitive requests may use an external licensed model when policy permits. 

The system must never silently route a sensitive request externally if the internal model becomes unavailable. 

6.7 Audit Visibility 

Authorized users can review: 

User identity 

Request time 

Data classification 

Retrieved sources 

Selected model 

Routing decision 

Policy outcome 

Recommendation status 

6.8 Human Decision Control 

AI provides decision support. 

Ticket modifications, regulated decisions, scientific approvals, quality approvals, and high-impact actions remain under authorized human control. 

 
 

7. Product Principles 

Existing enterprise systems remain the source of truth. 

Authorization is enforced before retrieval. 

Sensitive or uncertain requests fail closed. 

AI recommendations must include reasons and evidence. 

Derived knowledge inherits the controls of its source. 

AI must not autonomously approve high-impact decisions. 

Model prompts are not treated as a security boundary. 

Continuous AI processes must have clear limits and stopping conditions. 

Models and data stores must remain replaceable. 

Human owners remain accountable for final decisions. 

 
 

8. High-Level Architecture 

Users 
Developer | Scientist | Support | Quality | Manager | Administrator 
                               | 
                         Web Interface 
                               | 
                   Enterprise Identity / SSO 
                               | 
                         Secure API Gateway 
                               | 
       +-----------------------+-----------------------+ 
       |                       |                       | 
Prompt/Data Classifier    Policy Engine          Audit Service 
       |                       |                       | 
       +-----------------------+-----------------------+ 
                               | 
                        AI Orchestrator 
             +-----------------+-----------------+ 
             |                 |                 | 
       RAG Retriever      Model Router      Looping Engine 
             |                 |                 | 
        ACL Filter        +----+----+       Ticket Analysis 
             |            |         |       Background Tasks 
             |         Internal   Approved 
             |           LLM      External LLM 
             | 
     +-------+-----------------------+ 
     |                               | 
Knowledge Index              Metadata / ACL Store 
     |                               | 
     +---------------+---------------+ 
                     | 
              Ingestion Pipeline 
                     | 
     Code | Documents | Tickets | SOPs | Service Knowledge 
 

Architecture Boundary 

The model does not directly access source systems. 

All access passes through controlled services responsible for identity, permissions, policy enforcement, retrieval, routing, and auditing. 

 
 

9. Typical Request Flow 

1. User signs in through enterprise identity. 
2. The user submits a prompt or ticket for analysis. 
3. The platform classifies the request and its data sensitivity. 
4. The policy engine determines permitted sources and models. 
5. The retrieval layer applies user and document permissions. 
6. Authorized knowledge is retrieved. 
7. The model router selects an approved model. 
8. The model generates a grounded response. 
9. The response is returned with citations and limitations. 
10. The routing and policy decisions are recorded for audit. 
 
 

10. Proposed Technology Stack 

The final stack depends on Waters infrastructure and architecture review. 

Application 

React or Next.js 

Fluent UI 

Python with FastAPI 

REST APIs with streaming responses 

AI and Orchestration 

Semantic Kernel, LangGraph, or lightweight custom orchestration 

Ollama for local development 

vLLM for production internal model serving 

Approved internal and external model adapters 

Retrieval and Data 

PostgreSQL with pgvector or Qdrant 

Local or approved embedding model 

Hybrid keyword and vector search 

PostgreSQL for policy, ACL, and application metadata 

Identity and Security 

Microsoft Entra ID 

OAuth 2.0 and OpenID Connect 

Azure Key Vault, HashiCorp Vault, or approved secrets management 

TLS, private endpoints, and restricted network egress 

Deployment and Monitoring 

Docker Compose for development 

Kubernetes or OpenShift for production 

OpenTelemetry, Prometheus, and Grafana 

Waters-controlled on-premises or approved hybrid infrastructure 

 
 

11. Codebase Structure 

A modular monorepo can keep the initial platform manageable. 

waters-ai-vault/ 
| 
+-- apps/ 
|   +-- web/                    # User and admin interface 
|   +-- api/                    # FastAPI endpoints 
|   +-- worker/                 # Ingestion and background jobs 
| 
+-- services/ 
|   +-- policy/                 # Classification and policy enforcement 
|   +-- retrieval/              # Search and permission filtering 
|   +-- model-router/           # Internal and external model routing 
|   +-- ticket-intelligence/    # Ticket analysis 
|   +-- looping-engine/         # Continuous background analysis 
|   +-- audit/                  # Audit event handling 
|   +-- evaluation/             # AI security and quality checks 
| 
+-- connectors/ 
|   +-- sharepoint/ 
|   +-- azure-devops/ 
|   +-- github/ 
|   +-- servicenow/ 
|   +-- file-ingestion/ 
| 
+-- packages/ 
|   +-- contracts/              # Shared schemas 
|   +-- security/               # Shared authorization utilities 
|   +-- prompts/                # Version-controlled prompts 
|   +-- telemetry/              # Logs, traces and metrics 
| 
+-- infrastructure/ 
|   +-- docker/ 
|   +-- kubernetes/ 
|   +-- monitoring/ 
| 
+-- tests/ 
|   +-- unit/ 
|   +-- integration/ 
|   +-- security/ 
| 
+-- docs/ 
|   +-- architecture/ 
|   +-- decisions/ 
| 
+-- README.md 
+-- docker-compose.yml 
 
 

12. Scope Boundaries 

Waters AI Vault will not initially: 

Replace existing ticketing or document-management systems. 

Train a foundation model from scratch. 

Provide unrestricted access to internal repositories. 

Automatically modify ticket priorities. 

Autonomously approve scientific, quality, safety, or regulatory decisions. 

Control laboratory instruments. 

Treat AI-generated content as an authoritative record. 

Send sensitive content to external AI services. 

Run unrestricted AI agents without resource and action limits. 

 
 

13. Key Risks 

13.1 On-Premises Cost 

GPU infrastructure, model operations, power, maintenance, and specialist support may cost more than expected. 

13.2 Model Capability 

Smaller internal models may not provide sufficient quality for complex scientific or engineering tasks. 

13.3 Prompt Injection 

Malicious instructions may enter through user prompts, tickets, documents, code comments, or uploaded files. 

13.4 Permission Leakage 

Incorrect ACL synchronization or retrieval filtering may expose restricted information. 

13.5 Secondary Knowledge Leakage 

Generated summaries or embeddings may reveal protected information even when raw documents remain restricted. 

13.6 Incorrect Recommendations 

AI may misunderstand release context, dependencies, or business impact and recommend the wrong ticket priority. 

13.7 Continuous Loop Failure 

Background AI processes may create repeated alerts, unnecessary compute usage, or unreliable feedback loops. 

13.8 Increased Platform Complexity 

The solution may introduce another enterprise platform that requires infrastructure, governance, security, support, and long-term ownership. 

 
 

14. Uncertainties 

14.1 On-Premises Feasibility 

Will running AI on-prem be technically and financially feasible? 

This depends on expected usage, model size, GPU availability, latency requirements, support ownership, and whether a hybrid deployment is acceptable. 

14.2 Internal Knowledge Access 

Will it be secure to connect AI with our internal knowledge base through permission-aware RAG? 

The solution is viable only if source permissions are preserved, authorization happens before retrieval, and derived knowledge remains governed. 

14.3 Business Value 

Are we solving a real business problem, or introducing more security risk, infrastructure cost, and operational complexity? 

The platform should proceed only when a focused use case shows measurable improvement over existing search, ticketing, and knowledge-management tools. 

 
 

15. Product Positioning 

Waters AI Vault is a secure enterprise intelligence platform that connects authorized employees with protected engineering, scientific, operational, and business knowledge. It provides cited AI assistance, controlled model routing, and explainable work recommendations while preserving existing permissions, authoritative systems, and human decision ownership. 