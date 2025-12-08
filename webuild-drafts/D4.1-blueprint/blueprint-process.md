# Blueprint work process

**Authors:**  
- Sarah Amandusson, Digg, Sweden

## Context
<!-- What is forcing us to make this decision? What was the tradeoff? -->
To assemble the  [D4.1 Architecture & Integration Blueprint Reference Document](./architecture-integration-blueprint-reference-document.md) ("Blueprint"), we draw upon the existing outputs and governance structures of the **Architectural Decision Record (ADR)** and **Conformance Specification (CS)** processes.  
The Blueprint is not a parallel process - it consolidates the architectural reasoning captured in ADRs and the implementation definitions established in CS documents into a single, strategic reference.

The following aspects must be considered when developing the Blueprint:

1. **Hierarchy of Inputs**  
The Blueprint builds on the decisions formally captured in ADRs and the interface and implementation requirements defined through the CS process. It combines these artefacts into a cohesive high-level framework for the project.

2. **Rationale and Alignment**  
   The Blueprint must clearly reflect how the architecture aligns with overarching mandates — particularly the eIDAS Regulation, implementing acts, and the  Architectural Reference Framework (ARF) - as captured through ADRs and CS.

3. **Integration of WP4 Contributions**  
   The Blueprint synthesizes the outputs from the various WP4 capability groups (e.g. Semantics, Wallet Providers, Trust Registry, Testing, PID/LPID, QTSPs) to ensure interoperability and traceability across all components.

4. **Use Case Requirements**  
   The Blueprint integrates the requirements and findings gathered from WP2 and WP3 use cases (stocktaking and pilot design phases) to ensure that architectural decisions and conformance definitions serve actual implementation needs.

## Decision
The consortium agrees that the Architecture & Integration Blueprint (D4.1) will be developed by synthesizing and structuring the outputs of the existing Architectural Decision Record (ADR) and Conformance Specification (CS) processes.  

The **Blueprint Coordination Group** ([@webuild-consortium/blueprint-coordination-group](https://github.com/orgs/webuild-consortium/teams/blueprint-coordination-group)) is assigned responsibility for maintaining and approving the Blueprint content.  

 **Specifically, the group shall:**
- Review and approve incoming ADR pull requests that affect architectural scope or integration requirements.  
- Ensure that approved ADRs and CSs are consistently reflected in the Blueprint.  
- Review Conformance Specifications
- Maintain the Blueprint as a living document and coordinate updates across WP4 capability groups.

The Blueprint thus serves as the single, high-level reference for the project’s architecture — simplifying governance and ensuring traceability between architectural reasoning (ADRs), implementation specifications (CSs), and the overarching project framework.

## Consequences

**Positive outcomes**
- Ensures coherence and traceability: every architectural statement in the Blueprint can be traced to specific ADRs or CSs.  
- Simplifies governance: the Blueprint becomes the single reference for understanding how decisions and specifications connect.  
- Encourages consistency across capability groups by aligning architecture and conformance in one integrated view.  
- Makes communication easier - especially for external stakeholders and regulators - since the Blueprint reflects verified, consortium-approved artefacts.

**Challenges / trade-offs**
- Requires disciplined updates: whenever ADRs or CSs evolve, the Blueprint must be revised to stay current.  
- The editorial responsibility for maintaining alignment may need to be adjusted.  
- Early drafts may lag slightly behind the most recent technical changes until processes stabilize.

**Risk mitigation**
- Introduce a lightweight “sync checkpoint” (e.g., monthly or at each workshop) to verify that new ADRs and CSs are reflected in the Blueprint.  
- Assign explicit ownership for updating and validating cross-references.

## Advice

Once merged, this is our consortium’s decision. This does not mean all
participants agree it is the best possible decision. In the decision
making process, we have heard the following advice.

- yyyy-mm-dd, Name, Affiliation, Country: OK or summary of advice
