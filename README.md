# Vendor Onboarding AI

## Overview
**Vendor Onboarding AI** is a repository-based AI instruction pack designed to streamline and standardise the initial review of vendor registration documents. The project guides AI coding agents and human reviewers in verifying document submission completeness, identifying missing mandatory records, calculating completeness percentages, and preparing structured compliance summaries for procurement teams.

This project is developed as part of **Session 8 of the Korefield Academy AI Builder Programme**: *From Custom Assistants to Portable, Version-Controlled AI Instructions*.

---

## Target Users
- **Procurement & Sourcing Teams**: Quickly check new supplier onboarding submissions before manual vetting.
- **Vendor Onboarding Officers**: Identify missing compliance records and communicate requirements back to vendors.
- **Compliance Reviewers**: Ensure strict segregation between administrative completeness and substantive legal validation.
- **AI Builders & Developers**: Use portable instructions (`AGENTS.md`, `SKILL.md`) to guide AI coding assistants in building and testing document workflows.

---

## Features
- **Required Document Verification**: Checks submitted vendor records against standardized procurement compliance checklists.
- **Missing Document Identification**: Flags missing mandatory records (e.g., Certificate of Incorporation, Tax Compliance Certificate, Bank Confirmation).
- **Completeness Percentage Calculation**: Computes mathematically accurate, duplicate-resilient submission rates:
  $$\text{Completeness (\%)} = \left(\frac{\text{Submitted Required Documents}}{\text{Total Required Documents}}\right) \times 100$$
- **Structured Status Reporting**: Produces consistent, audit-ready summaries detailing review statuses.
- **Mandatory Human Escalation**: Automatically routes incomplete submissions or ambiguous records to human procurement officers.

---

## Limitations
This demonstration instruction pack explicitly enforces:
- **No Automatic Vendor Approval**: Completeness does *not* imply authenticity, creditworthiness, or legal compliance.
- **No Direct Production System Access**: Operates strictly within isolated development/testing sandboxes.
- **No Use of Real Personal or Corporate Data**: All tests and examples rely strictly on synthetic mock data.
- **No Legal or Regulatory Validation**: The AI assesses only document presence, not legal validity or authenticity.

---

## Project Structure
```text
vendor-onboarding-ai/
│
├── README.md                           # Project overview, purpose, and guidance
├── AGENTS.md                           # Universal instructions and boundaries for AI coding agents
├── REFLECTION.md                       # Assignment reflection and architecture analysis
├── .gitignore                          # Prevents committing secrets, environment files, and artifacts
│
├── skills/                             # Portable, reusable AI agent skills
│   ├── compliance-check/
│   │   └── SKILL.md                    # Core skill: document completeness & missing-item verification
│   └── report-generation/
│       └── SKILL.md                    # Reporting skill: audit summaries & escalation alerts
│
├── rules/                              # Policy documents and environment-specific standards
│   ├── security-rules.md               # Secrets protection, prompt injection defence, least privilege
│   └── tool-specific-rules.md          # Coding conventions (Python/PEP 8), testing (pytest), git rules
│
├── logs/                               # Audit trails and execution history
│   └── task-log.md                     # Structured records of AI-assisted tasks
│
└── tests/                              # Synthetic test suites and evaluation results
    └── test-cases.md                   # Benchmark cases (Alpha, Beta, Gamma, Delta Ltd) & results
```

---

## Getting Started

### 1. Clone the Repository
```bash
git clone https://github.com/martinktay/vendor-onboarding-ai.git
cd vendor-onboarding-ai
```

### 2. Inspect Repository Instructions
- Review [`AGENTS.md`](file:///AGENTS.md) to understand agent boundaries, security constraints, and execution guidelines.
- Inspect [`skills/compliance-check/SKILL.md`](file:///skills/compliance-check/SKILL.md) for the document checklist calculation logic.
- Review [`rules/security-rules.md`](file:///rules/security-rules.md) for data handling and credential hygiene.

### 3. Run Synthetic Verification
Evaluate the test cases documented in [`tests/test-cases.md`](file:///tests/test-cases.md) to confirm that the assistant correctly flags incomplete submissions and never auto-approves vendors.

---

## Project Status
**Version 1.0.0 — Repository Instruction Pack Architecture**  
This release establishes the version-controlled instruction architecture. Executable Python automation scripts and API integrations will be implemented in subsequent phases (Session 9: Python Basics for AI Builders).
