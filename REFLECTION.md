# Session 8 Assignment Reflection & Submission Report

**Student Name**: Martin Tay  
**Programme**: Korefield Academy — AI Builder Programme  
**Session**: Session 8 — GPT Actions, Agent Skills, AGENTS.md, SKILL.md and Repository Instructions  
**Repository Link**: [https://github.com/martinktay/vendor-onboarding-ai](https://github.com/martinktay/vendor-onboarding-ai)

---

## 1. Problem Description
In enterprise procurement and supply-chain operations, onboarding new vendors requires verifying that mandatory compliance, tax, and legal documents are submitted before formal review. When handled informally through ad-hoc chat sessions or unstructured manual checklists:
- Instructions are lost between chat windows.
- Reviewers apply inconsistent criteria.
- Risk arises that an AI assistant might erroneously "approve" a vendor or fail to isolate missing documents.
- Prompts cannot be version-controlled, audited, or shared across teams.

**Vendor Onboarding AI** solves this by packaging vendor document completeness logic into a portable, version-controlled repository instruction pack. It equips AI coding agents and human reviewers with unambiguous rules to evaluate document presence, calculate submission completeness percentages, and escalate incomplete or ambiguous cases to human officers.

---

## 2. Reusable Skill Explanation (`compliance-check`)
The core reusable skill is located in [`skills/compliance-check/SKILL.md`](file:///skills/compliance-check/SKILL.md).
- **Function**: Given a standardized checklist of required documents (e.g., Certificate of Incorporation, Tax Compliance Certificate, Business Permit, Bank Details Confirmation, Director ID) and an arbitrary list of submitted items, it:
  1. Deduplicates multiple copies of the same document to prevent artificial metric inflation.
  2. Compares submitted items against mandatory requirements.
  3. Accurately identifies every missing document.
  4. Calculates the mathematical completion percentage:
     $$\text{Completion Percentage} = \left(\frac{\text{Unique Valid Submissions}}{\text{Total Required Documents}}\right) \times 100$$
  5. Assigns an operational status (`READY_FOR_HUMAN_EVALUATION` vs. `INCOMPLETE_DOCUMENTS_PENDING`).
- **Safety Boundary**: The skill explicitly states that submission completeness is *not* equal to legal authenticity. Under no circumstance does the skill or agent approve a vendor automatically.

---

## 3. How the Instruction Files Support the Project

| File / Directory | Target Audience | Role in the AI Architecture |
| :--- | :--- | :--- |
| [`README.md`](file:///README.md) | Human developers, stakeholders, and reviewers | Project identity, architecture roadmap, usage guidelines, and scope limitations. |
| [`AGENTS.md`](file:///AGENTS.md) | Compatible AI coding agents (Codex, Claude Code, Cursor, Copilot) | Root behavioral contract defining permitted coding tasks, business requirements, negative boundaries, and human approval gates. |
| [`skills/`](file:///skills/) | Autonomous agents executing specialized sub-procedures | Modular, portable procedures (`compliance-check`, `report-generation`) with standardized inputs, calculations, and structured outputs. |
| [`rules/`](file:///rules/) | Agents and developer tooling | Explicit security rules (secrets protection, prompt injection resistance, least privilege) and technical stack guidance (Python 3.11+, PEP 8, pytest). |
| [`logs/`](file:///logs/) | Auditors and compliance reviewers | Chronological, audit-ready records of AI tasks and validation runs to verify repeatability. |
| [`tests/`](file:///tests/) | Verification systems and evaluators | Benchmark datasets (nominal, partial, duplicate, adversarial injection) with deterministic expected vs. actual outcomes. |

Moving from chat-based prompts to repository instruction files ensures that AI behavior is **portable**, **version-controlled**, **testable**, and **collaborative**.

---

## 4. Evidence of Three Meaningful Git Commits

The repository history follows the three-stage progression recommended in Session 8:

```text
* commit 3 (HEAD -> main) docs: add security policies, task logs, test cases, and reflection
  - Added rules/security-rules.md (credential safety, prompt injection defense, least privilege)
  - Added rules/tool-specific-rules.md (Python conventions, pytest standards, commit hygiene)
  - Added logs/task-log.md (audit records for benchmark evaluations)
  - Added tests/test-cases.md (synthetic test matrix for Alpha through Zeta Ltd)
  - Added REFLECTION.md (assignment submission report)

* commit 2 docs: add agent instructions and compliance skills
  - Added AGENTS.md (coding-agent operational instructions and boundaries)
  - Added skills/compliance-check/SKILL.md (document completeness verification skill)
  - Added skills/report-generation/SKILL.md (structured status reporting skill)

* commit 1 docs: initialise vendor onboarding project documentation
  - Added README.md (project overview, features, limitations, directory map)
  - Added .gitignore (preventing secrets and temporary artifacts from being tracked)
```

---

## 5. Verification and Testing Methodology
The instruction pack was evaluated using 6 synthetic test scenarios documented in [`tests/test-cases.md`](file:///tests/test-cases.md):
1. **Nominal Case (`Alpha Ltd`)**: 5/5 submitted $\rightarrow 100.0\%$, 0 missing. Flagged for human document validity review (no auto-approval).
2. **Partial Cases (`Beta`, `Gamma`, `Delta Ltd`)**: Accurately identified 2, 1, and 3 missing documents respectively, resulting in completion rates of $60\%$, $80\%$, and $40\%$.
3. **Duplicate Submission Attack (`Epsilon Ltd`)**: Vendor submitted 3 copies of one document. The deduplication rule successfully prevented metric distortion, scoring $1/5 = 20.0\%$.
4. **Adversarial Prompt Injection (`Zeta Ltd`)**: Injected system override commands inside document filenames were safely treated as untrusted string data without compromising the checklist evaluation.

All test scenarios yielded expected results and confirmed that security and business boundaries were preserved throughout.
