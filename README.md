<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>

# Osmosis

**Osmosis** is an AI-assisted engineering initiative designed to reduce the time teams spend understanding defects, finding relevant technical knowledge, identifying likely root causes, and reusing confirmed solutions.

The repository contains two Product Requirements Documents representing the evolution of the same product idea:

- **[S1: Osmosis - Analysis and Engineering Loop - PRD](./documents/prd-s1/osmosis-prd-s1.md)** describes the current, focused direction for Digital Commerce defect analysis.
- **[G1: Osmosis - Knowledge and Engineering Loop - PRD](./documents/prd-g1/osmosis-prd-g1.md)** preserves the original, broader enterprise AI and knowledge-platform vision.

S1 and G1 are version labels used to distinguish the two stages of the concept. **S1 is the current product direction**, while **G1 provides the original context and longer-term vision from which S1 was developed.**

## Product Positioning

Osmosis is an evidence-backed engineering intelligence loop for Digital Commerce.

The product connects defect reports with authorized engineering knowledge, including previous defects, pull requests, code changes, logs, test results, deployments, documentation, and confirmed solutions. Osmosis uses this context to suggest likely root causes, investigation steps, possible resolutions, and validation tests while keeping engineers responsible for all final decisions.

The current concept is built around two main components:

- **AI Evaluation Harness:** evaluates the accuracy, evidence grounding, reliability, and usefulness of AI-generated defect analysis.
- **Looping Engineering Engine:** learns from resolved defects, engineer feedback, confirmed root causes, and implemented solutions to improve future analysis.

The initial focus areas are:

- eProcurement
- Kerberos
- Customer Onboarding


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>



## S1: Current Focused Direction

The S1 version narrows Osmosis to a specific and measurable Digital Commerce problem: the engineering effort required to identify, analyze, and resolve defects.

### S1 Objective

Help engineers begin defect investigation faster by connecting a reported issue with relevant engineering evidence and previously confirmed knowledge.

### S1 Idea

When a defect is raised, Osmosis collects the available authorized context and produces an evidence-backed analysis that can include:

- A clear summary of the problem and affected area
- Similar historical defects and confirmed solutions
- Potentially related pull requests and system changes
- Ranked root-cause hypotheses with supporting evidence
- Recommended investigation and resolution steps
- Suggested validation and regression tests
- Confidence, missing evidence, and known limitations

An engineer reviews the analysis, investigates the issue, and implements the final fix. The confirmed root cause, solution, test results, and engineer feedback then become inputs to the learning process.

The **AI Evaluation Harness** checks whether the analysis is accurate, grounded, and useful. The **Looping Engineering Engine** uses validated outcomes to improve how future defects are analyzed.

**Read the current S1 PRD:** [s1.md](./documents/prd-s1/osmosis-prd-s1.md)


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>


## G1: Original Broader Vision

The G1 version represents the original Osmosis concept. It positioned the product as a secure enterprise AI and knowledge platform serving engineering, science, service, quality, and business functions.

### G1 Objective

Provide a governed intelligence layer across internal repositories and enterprise systems so employees can securely discover and use organizational knowledge.

### G1 Idea

The original concept included a broader set of platform capabilities:

- Secure access to enterprise knowledge
- Permission-aware retrieval and cited responses
- Internal and external AI model routing
- Ticket intelligence and prioritization
- Cross-department knowledge discovery
- Continuous AI assistance
- Centralized governance, security, and auditing

G1 established the long-term knowledge vision, but it attempted to address several organizational problems and platform capabilities at the same time. S1 was created to validate the core value through one focused engineering use case before considering broader expansion.

**Read the original G1 PRD:** [g1.md](./documents/prd-g1/osmosis-prd-g1.md)


<img src="https://capsule-render.vercel.app/api?type=soft&color=gradient&height=10&section=header" width="1080" align="center"/>
