<!-- Sync Impact Report:
Version change: 0.0.0 → 1.0.0
Modified principles:
  - Spec-Driven Development (Added)
  - Prompt History Records (Added)
  - Architectural Decision Records (Added)
  - Small, Testable Changes (Added)
  - Human-in-the-Loop Interaction (Added)
Added sections:
  - Development Guidelines
  - Code Standards
Removed sections: None
Templates requiring updates:
  - .specify/templates/plan-template.md: ✅ updated
  - .specify/templates/spec-template.md: ✅ updated
  - .specify/templates/tasks-template.md: ✅ updated
  - .specify/templates/commands/sp.phr.md: ✅ updated
  - README.md: ⚠ pending
Follow-up TODOs: None
-->
# GIAIC Hackathon 1 Constitution

## Core Principles

### I. Spec-Driven Development (SDD)
Every feature, bug fix, or enhancement must begin with a clear, machine-readable specification (`spec.md`). This spec serves as the single source of truth for requirements and expected behavior, ensuring alignment across design, implementation, and testing. All work must trace back to an approved spec.

### II. Prompt History Records (PHRs)
Every significant user interaction, decision, and development step MUST be recorded as a Prompt History Record. PHRs provide an immutable audit trail, capture context, and enable learning from past exchanges. They are essential for traceability, debugging, and knowledge transfer within the project.

### III. Architectural Decision Records (ADRs)
Architecturally significant decisions, including major design choices, technology selections, and trade-offs, MUST be documented in Architectural Decision Records. ADRs provide transparency, capture rationale, and establish precedents for future development, promoting consistency and maintainability.

### IV. Small, Testable Changes
All code changes MUST be small, atomic, and independently testable. Prefer incremental modifications over large, monolithic changes. Each commit or pull request should address a single, well-defined problem or feature, making reviews easier, reducing the risk of regressions, and simplifying debugging.

### V. Human-in-the-Loop Interaction
The development process MUST incorporate explicit human review and approval at critical junctures. Automation supports, but does not replace, human judgment. Agents MUST surface key decisions, plans, and completed work for user confirmation, ensuring alignment and quality control.

## Development Guidelines

All agents MUST prioritize and use MCP tools and CLI commands for all information gathering and task execution. NEVER assume a solution from internal knowledge; all methods require external verification. Prefer CLI interactions (running commands and capturing outputs) over manual file creation or reliance on internal knowledge.

## Code Standards

Code quality, testing, performance, security, and architecture principles are derived from the overall SDD process and enforced through specifications and plans.

## Governance

This Constitution supersedes all other practices and documentation within the project. Amendments require a formal proposal, review, and approval process, documented in an ADR. Versioning follows semantic versioning rules (MAJOR.MINOR.PATCH). All PRs and code reviews must verify compliance with these principles.

**Version**: 1.0.0 | **Ratified**: 2026-04-17 | **Last Amended**: 2026-04-17