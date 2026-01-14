<!--
SYNC IMPACT REPORT - Constitution v1.0.0

VERSION CHANGE: [TEMPLATE] → 1.0.0
BUMP RATIONALE: Initial constitution ratification from template

PRINCIPLES DEFINED:
  ✓ I. Specification First - Feature specs must precede implementation
  ✓ II. Independent User Stories - Each story must be independently testable and deliverable
  ✓ III. Clarity & Documentation - All artifacts must be clear, measurable, and traceable
  ✓ IV. Dependency-Ordered Tasks - Tasks organized by phases with explicit parallelization
  ✓ V. Incremental Delivery - MVP-first approach with independent story validation

SECTIONS ADDED:
  ✓ Quality Standards - Measurable requirements and validation criteria
  ✓ Development Workflow - Spec → Plan → Tasks → Implement cycle
  ✓ Governance - Amendment procedures and compliance review

TEMPLATE CONSISTENCY STATUS:
  ✅ .specify/templates/spec-template.md - Aligned (user stories, priorities, testability)
  ✅ .specify/templates/plan-template.md - Aligned (constitution check gate, complexity tracking)
  ✅ .specify/templates/tasks-template.md - Aligned (user story phases, dependencies, parallelization)
  ⚠️  .specify/templates/checklist-template.md - Requires review for principle alignment
  ⚠️  .specify/templates/agent-file-template.md - Requires review for principle alignment

FOLLOW-UP TASKS:
  - Review checklist-template.md to ensure constitution principle checks are included
  - Review agent-file-template.md to ensure agent guidance aligns with constitution
  - Update command files in .claude/commands/ to reference specific principles by name

RECOMMENDED COMMIT MESSAGE:
  docs: ratify constitution v1.0.0 (5 principles + workflow standards)
-->

# SpecKit Constitution

## Core Principles

### I. Specification First

Every feature begins with a complete specification before any planning or implementation occurs. Specifications MUST include:

- Prioritized user stories (P1, P2, P3...) with clear acceptance criteria
- Functional requirements with explicit MUST/SHOULD clauses
- Measurable success criteria (technology-agnostic metrics)
- Edge cases and error scenarios
- Clear identification of unclear requirements using `[NEEDS CLARIFICATION: ...]` markers

**Rationale**: Prevents scope creep, ensures stakeholder alignment, and provides a single source of truth for what constitutes "done."

### II. Independent User Stories

Each user story MUST be independently testable, implementable, and deliverable as a standalone increment of value. This means:

- Story can be fully implemented without completing other stories
- Story can be tested and validated on its own
- Story delivers measurable user value even if other stories aren't complete
- P1 stories represent the minimum viable product (MVP)

**Rationale**: Enables parallel development, supports incremental delivery, reduces risk by allowing early validation, and ensures each story adds real value.

### III. Clarity & Documentation

All specifications, plans, and tasks MUST be clear, concrete, and free of ambiguity:

- NO vague language ("should probably", "might need", "could be")
- Replace with explicit MUST/SHOULD/MAY with rationale
- Every requirement must be measurable or verifiable
- Every entity must have clear attributes and relationships
- Every task must include exact file paths and concrete deliverables
- Unclear requirements flagged with `[NEEDS CLARIFICATION: ...]` rather than guessed

**Rationale**: Reduces miscommunication, enables accurate estimation, facilitates handoffs, and ensures consistent interpretation across teams and tools.

### IV. Dependency-Ordered Tasks

Task lists MUST be organized into explicit phases with clear dependencies and parallelization opportunities:

- **Setup Phase**: Project initialization (no dependencies)
- **Foundational Phase**: Core infrastructure that blocks all user stories (depends on Setup)
- **User Story Phases**: One phase per story in priority order (each depends on Foundational)
- **Polish Phase**: Cross-cutting improvements (depends on completed stories)
- Tasks marked `[P]` can run in parallel within a phase
- Tasks marked `[Story]` are traceable to specific user stories

**Rationale**: Maximizes parallel work, clarifies critical path, prevents blocking dependencies, and enables efficient resource allocation.

### V. Incremental Delivery

Features MUST be delivered incrementally following an MVP-first strategy:

- Complete foundational infrastructure first
- Implement P1 user story(s) to create MVP
- Validate MVP independently before proceeding
- Add P2, P3... stories as independent increments
- Each story checkpoint validates story works standalone

**Rationale**: Reduces risk through early validation, enables faster time-to-value, supports agile pivots based on feedback, and prevents big-bang integration failures.

## Quality Standards

### Specification Quality Gates

Before planning begins, specifications MUST pass these gates:

- ✅ At least one P1 user story defined with acceptance criteria
- ✅ All functional requirements have FR-### identifiers
- ✅ Success criteria are measurable and technology-agnostic
- ✅ Edge cases explicitly documented or marked as NEEDS CLARIFICATION
- ✅ All unclear requirements flagged rather than assumed

### Plan Quality Gates

Before task generation begins, implementation plans MUST pass these gates:

- ✅ Constitution Check section completed (validates alignment with principles)
- ✅ Technical context fully specified or marked NEEDS CLARIFICATION
- ✅ Project structure chosen and documented (single/web/mobile)
- ✅ Complexity tracking table filled if any constitution violations exist
- ✅ All placeholders replaced with concrete values

### Task Quality Gates

Before implementation begins, task lists MUST pass these gates:

- ✅ Tasks organized by user story phases (not arbitrary groupings)
- ✅ Foundational phase clearly separates blocking infrastructure
- ✅ Each task includes exact file paths (no "TBD" or vague locations)
- ✅ Parallel opportunities marked with [P] flag
- ✅ Story dependencies documented in Dependencies section
- ✅ Each user story has independent test checkpoint

## Development Workflow

### Standard Workflow Sequence

1. **Specify**: `/speckit.specify` - Create or update feature specification
   - Output: `specs/###-feature/spec.md`
   - Gate: Must pass Specification Quality Gates

2. **Clarify** (optional): `/speckit.clarify` - Ask targeted questions for underspecified areas
   - Updates: `specs/###-feature/spec.md` with answers encoded

3. **Plan**: `/speckit.plan` - Generate implementation plan and design artifacts
   - Output: `specs/###-feature/plan.md`, `research.md`, `data-model.md`, `contracts/`, `quickstart.md`
   - Gate: Must pass Plan Quality Gates

4. **Tasks**: `/speckit.tasks` - Generate dependency-ordered task list
   - Output: `specs/###-feature/tasks.md`
   - Gate: Must pass Task Quality Gates

5. **Implement**: `/speckit.implement` - Execute tasks in dependency order
   - Input: All artifacts from steps 1-4
   - Process: Follows task dependencies, validates checkpoints

6. **Validate**: Manual or automated validation against success criteria
   - Verify P1 story(s) work independently (MVP validation)
   - Verify each additional story works independently
   - Run quickstart.md instructions to confirm end-to-end flow

### Optional Workflow Extensions

- **Checklist**: `/speckit.checklist` - Generate custom validation checklist
- **Analyze**: `/speckit.analyze` - Cross-artifact consistency analysis
- **Constitution**: `/speckit.constitution` - Update project principles (this document)

## Governance

### Amendment Authority

This constitution governs all feature development within SpecKit. Changes require:

1. Documented rationale for the change
2. Impact analysis on existing templates and workflows
3. Version bump following semantic versioning:
   - **MAJOR**: Backward incompatible changes (principle removal, redefinition)
   - **MINOR**: New principles or sections added
   - **PATCH**: Clarifications, wording improvements, typo fixes

4. Sync Impact Report documenting:
   - Template changes required
   - Command file updates needed
   - Migration plan for in-flight features

### Compliance Review

All artifacts generated by SpecKit commands MUST verify compliance with this constitution:

- Specifications checked against Principle I (Specification First) and Principle III (Clarity)
- Plans checked against Principle II (Independent User Stories) via Constitution Check section
- Tasks checked against Principle IV (Dependency-Ordered) and Principle V (Incremental Delivery)
- Implementation follows task order and validates story checkpoints

### Complexity Justification

Any violation of constitution principles MUST be justified in the plan's Complexity Tracking table:

- **Violation**: Which principle is being violated
- **Why Needed**: Specific technical or business constraint requiring the violation
- **Simpler Alternative Rejected Because**: Why a compliant approach was insufficient

Violations without justification indicate plan defects requiring revision.

**Version**: 1.0.0 | **Ratified**: 2026-01-11 | **Last Amended**: 2026-01-11
