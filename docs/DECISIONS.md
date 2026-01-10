# Decision Log

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** Record of key design decisions and rationale

---

## Overview

This document records important design decisions, their rationale, and their impact. Decisions are recorded when they:

- Establish patterns that affect multiple workflows
- Define constraints or boundaries
- Resolve tradeoffs between approaches
- Set precedents for future decisions

---

## Decision Format

Each decision entry follows this structure:

```markdown
### Decision: [Short Title]

**Date:** YYYY-MM-DD  
**Status:** [Active | Superseded | Deprecated]  
**Context:** [What situation led to this decision]

**Decision:**
[What was decided]

**Rationale:**
[Why this decision was made]

**Alternatives Considered:**
[Other options that were considered and why they were rejected]

**Impact:**
[What this decision affects, constraints it creates, patterns it establishes]

**Review:**
[When/how this decision should be reviewed]
```

---

## Core Decisions

### Decision: Role Fidelity Over Helpfulness

**Date:** 2026-01-09  
**Status:** Active  
**Context:** Agents tend to be overly helpful, blurring role boundaries

**Decision:**
Agents must prioritize staying within their role boundaries over being helpful. If a request falls outside an agent's role, the agent must redirect to the appropriate agent rather than handling it themselves.

**Rationale:**
- Prevents scope creep and ambiguity
- Maintains clear accountability
- Ensures predictable agent behavior
- Creates sustainable context management

**Alternatives Considered:**
- Allow agents to be flexible when helpful: Rejected because it creates ambiguity and drift
- Expand all agent roles: Rejected because it dilutes specialization

**Impact:**
- Agents must know all roles and routing patterns
- Requires explicit escalation protocols
- May feel less "helpful" in short term
- Creates sustainable long-term patterns

**Review:**
Review when role boundaries become too restrictive or unclear

---

### Decision: Documentation as Truth

**Date:** 2026-01-09  
**Status:** Active  
**Context:** Documentation often drifts from actual behavior

**Decision:**
Documentation is treated as the authoritative source of truth. When behavior changes, documentation must be updated immediately. Documentation without current version/date is considered invalid.

**Rationale:**
- Prevents context confusion
- Ensures agents have accurate information
- Creates accountability for keeping docs current
- Enables reliable decision-making

**Alternatives Considered:**
- Documentation as reference only: Rejected because it allows drift
- Periodic documentation updates: Rejected because it creates windows of inaccuracy

**Impact:**
- Requires discipline to update docs on every change
- Documentation updates are mandatory, not optional
- Changelog entries required for all system changes
- Documentation freshness validation needed

**Review:**
Review if maintenance burden becomes too high

---

### Decision: Brief as Single Source of Truth

**Date:** 2026-01-09  
**Status:** Active  
**Context:** Requirements often communicated verbally, leading to ambiguity

**Decision:**
All implementation work must be based on a written brief. The brief is the single source of truth for intent. CB must not infer missing intent or accept verbal clarifications.

**Rationale:**
- Eliminates ambiguity in requirements
- Creates audit trail of decisions
- Prevents scope creep
- Enables reliable handoffs

**Alternatives Considered:**
- Allow verbal clarifications: Rejected because it creates ambiguity
- Allow CB to infer intent: Rejected because it leads to scope creep

**Impact:**
- TB must create complete briefs
- Briefs must be unambiguous
- CB must escalate if brief is unclear
- All decisions must be explicit in brief

**Review:**
Review if brief creation becomes bottleneck

---

### Decision: Structured Handoff Artifacts

**Date:** 2026-01-09  
**Status:** Active  
**Context:** Agent handoffs often lack sufficient context

**Decision:**
All agent handoffs must use structured artifacts (briefs, findings) with explicit formats. Artifacts must be standalone (no external references needed) and include sufficient context.

**Rationale:**
- Ensures context preservation
- Enables reliable handoffs
- Creates audit trail
- Prevents information loss

**Alternatives Considered:**
- Verbal handoffs: Rejected because context is lost
- Minimal artifacts: Rejected because insufficient context

**Impact:**
- Requires structured artifact formats
- Artifacts must be comprehensive
- Storage and organization of artifacts needed
- Artifacts become historical record

**Review:**
Review if artifact formats become too rigid or insufficient

---

### Decision: SYSTEM_BUDDY Does Not Execute

**Date:** 2026-01-09  
**Status:** Active  
**Context:** SYSTEM_BUDDY could implement fixes directly, bypassing TB/CB workflow

**Decision:**
SYSTEM_BUDDY only observes, analyzes, and documents findings. All fixes must flow through: SYSTEM → findings → TB → brief → CB → implementation.

**Rationale:**
- Maintains role boundaries
- Ensures TB validates recommendations
- Prevents SYSTEM from making implementation decisions
- Creates proper separation of concerns

**Alternatives Considered:**
- Allow SYSTEM to implement directly: Rejected because it bypasses TB validation
- SYSTEM creates briefs: Rejected because brief creation requires intent clarification (TB's role)

**Impact:**
- SYSTEM findings must be actionable for TB
- TB validates all SYSTEM recommendations
- Longer feedback loop but higher quality
- Clear separation: analysis vs implementation

**Review:**
Review if feedback loop becomes too slow

---

### Decision: Changelog Discipline

**Date:** 2026-01-09  
**Status:** Active  
**Context:** System changes accumulate without clear record

**Decision:**
Every system change must have a changelog entry in SYSTEM_SUMMARY.md. Entry must include: version, date, status, what changed, why, impact, files modified.

**Rationale:**
- Creates complete history
- Enables informed decision-making
- Documents rationale for changes
- Provides audit trail

**Alternatives Considered:**
- Periodic changelog updates: Rejected because details are lost
- No changelog: Rejected because history is valuable

**Impact:**
- Requires discipline to log every change
- SYSTEM_SUMMARY.md grows over time
- Historical record becomes comprehensive
- Enables pattern recognition in changes

**Review:**
Review if changelog becomes too long or maintenance burden too high

---

### Decision: Version and Date on All Docs

**Date:** 2026-01-09  
**Status:** Active  
**Context:** Documentation freshness is hard to validate without version tracking

**Decision:**
All documentation files must have "Version" and "Last Updated" fields at the top. These must be updated on every edit. Documentation without current version/date is considered invalid.

**Rationale:**
- Enables freshness validation
- Creates accountability
- Prevents outdated information
- Signals when docs need review

**Alternatives Considered:**
- No version tracking: Rejected because can't validate freshness
- Version only: Rejected because date is also needed for context

**Impact:**
- Requires discipline to update on every edit
- All docs must follow header format
- Validation can check version/date
- Creates maintenance overhead

**Review:**
Review if maintenance burden becomes too high

---

## Notes

- Decisions establish patterns and constraints
- Decisions can be superseded but should be documented
- Review decisions periodically to ensure they're still appropriate
- New decisions should reference existing decisions when relevant

