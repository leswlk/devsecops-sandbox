# DevSecOps Blueprint Sandbox

![Pipeline Target](https://img.shields.io/badge/Pipeline--Target-pygoat--github--actions-ff69b4?style=flat-square&logo=github)
![Security Guardrails](https://img.shields.io/badge/Control--Plane-Decoupled%20Architecture-blue?style=flat-square&logo=githubactions)
![OSSF Compliance](https://img.shields.io/badge/OSSF--Scorecard-Tier%202%20Validated-success?style=flat-square&logo=securityscorecard)

This repo serves as a centralized Security Control Plane and architectural lab for reusable, enterprise-grade CI/CD security configurations, policy-as-code definitions, and supply chain guardrails.

Rather than running unchecked automation, these workflows are actively validated, fine tuned, and tested against a living, highly vulnerable deployment target application: [pygoat-github-actions](https://github.com/leswlk/pygoat-github-actions)

---

Topology & Feedback Loop

To preserve engineering throughput without degrading security assurance, this ecosystem decouples rapid feedback checks at the pull request gate from heavy, end-to-end runtime assessments during delivery.

```
  [ Developer PR Push ] 
           │
           ▼
 ┌────────────────────────────────────────────────────────┐
 │ 1. PRE-FLIGHT GUARD (Fast Feedback Loop < 2 mins)      │
 │    - Gitleaks (Passive Pre-Commit/Secret Interception) │
 │    - Semgrep (Lightweight AST Pattern Matching)        │
 └────────────────────────────────────────────────────────┘
           │
      (PR Approved) ──► Merge to Main Branch
           │
           ▼
 ┌────────────────────────────────────────────────────────┐
 │ 2. CONTINUOUS DELIVERY & RUNTIME ASSESSMENT            │
 │    - AWS CloudFormation Stack Provisioning             │
 │    - CodeQL (Deep Taint & Data-Flow Analysis)          │
 │    - OWASP ZAP (Authenticated DAST Target Assessment)  │
 └────────────────────────────────────────────────────────┘
