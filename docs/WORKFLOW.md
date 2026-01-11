# Workflow Patterns

**Version:** 1.3  
**Last Updated:** 2026-01-10  
**Purpose:** Detailed workflow patterns and collaboration protocols

---

## Overview

This document defines explicit workflow patterns for agent collaboration. These patterns ensure predictable behavior, clear handoffs, and sustainable context management.

---

## Core Workflows

### Brief Creation (THINKING_BUDDY)

**Trigger:**

- User provides vague or incomplete requirement
- User requests catch-up after manual edits
- User needs a feature or change implemented

**Process:**

1. TB consults `docs/project-context/` for relevant domain knowledge, business rules, or requirements (if applicable) - READ-ONLY reference, do not modify files in this folder unless explicitly requested
2. TB asks clarifying questions until ambiguity is zero
3. TB surfaces hidden assumptions and risks
4. TB forces explicit decisions on ambiguous points
5. TB identifies edge cases and failure modes
6. TB locks all decisions
7. TB creates brief with required structure
8. TB exports brief to `work/briefs/YYYY-MM-DD_name_brief.md`
9. TB stops and waits for user review/approval
10. User reviews brief (approves, requests changes, or cancels)
11. If approved: brief is ready for CB. If changes needed: TB revises and re-exports

### Why Two Agents? (TB and CB)

**This separation might look like overkill, but it solves real problems:**

**The Problem with One Agent:**

- Single agent mixes requirements thinking with implementation thinking
- Tends to jump to solutions before fully understanding the problem
- No clear checkpoint for user review before execution
- Scope creeps as agent "improves" things during implementation
- Hard to maintain accountability (who owns what?)
- Documentation gets skipped or done inconsistently

**The Solution: Two Agents with Clear Boundaries**

**THINKING_BUDDY (TB):**

- **Owns:** Intent, requirements, scope, decisions
- **Focus:** "What" and "Why" - understanding the problem completely
- **Output:** Brief (executable specification)
- **Stops:** After brief is created and approved

**CODING_BUDDY (CB):**

- **Owns:** Implementation quality, code execution
- **Focus:** "How" - executing from the brief
- **Input:** Brief (the contract)
- **Stops:** After implementation is complete

**Why This Works:**

1. **Cognitive Separation:** Different mental models - TB thinks about problems, CB thinks about solutions
2. **Quality Gate:** Brief serves as mandatory checkpoint - user reviews before execution
3. **Scope Control:** CB can't expand scope (it's not in the brief) - prevents feature creep
4. **Accountability:** Clear ownership - TB owns requirements, CB owns implementation
5. **User Control:** Brief gives you final say before any code is written
6. **Documentation:** Brief is permanent record - what was requested, what was built

**The Brief is the Contract:**

- TB creates it (requirements)
- You review it (approval)
- CB executes it (implementation)
- Brief documents it (history)

**Without this separation:**

- Agent guesses requirements while coding
- No clear checkpoint for review
- Scope expands during implementation
- Documentation is inconsistent
- Hard to track what was requested vs. what was built

### Why Briefs Exist

Briefs serve three critical functions:

**1. Role Separation and Responsibility:**

- TB owns intent, scope, and requirements (captured in brief)
- CB owns implementation quality and execution (from brief)
- Clear authority transfer: brief is the contract between roles
- Prevents scope creep and boundary blurring
- Each role has clear ownership and accountability

**2. User Review and Final Approval:**

- Brief gives user opportunity to review before execution
- User can approve, request changes, or cancel before CB starts
- Final checkpoint before implementation begins
- User has explicit "final say" on what will be built
- Prevents misunderstandings and unwanted features

**3. Documentation and History:**

- Brief documents the change/feature request permanently
- Implementation Notes (added by CB) document what was actually built
- Creates audit trail: why something was built, what was built, what changed
- Historical record for future reference and learning
- Enables understanding of system evolution over time

**Brief Requirements:**

- Context and goal
- Explicit requirements (no implicit assumptions)
- Non-goals (what is out of scope)
- Constraints and rules
- Acceptance criteria (measurable)
- Standards or processes to follow
- Testing expectations (if applicable)
- Documentation requirements
- Handoff note for CB

**Success Criteria:**

- Zero ambiguity in brief
- All decisions explicitly stated
- Scope clearly bounded
- CB can implement without asking questions
- User has reviewed and approved (or requested changes)

### Implementation (CODING_BUDDY)

**Trigger:** Receives approved brief from THINKING_BUDDY (after user review)

**Process:**

1. CB reads entire brief before acting
2. CB consults `docs/project-context/` for relevant domain knowledge or business rules (if applicable for the implementation) - READ-ONLY reference, do not modify files in this folder unless brief explicitly requests it
3. CB confirms internally: goal, scope, constraints, acceptance criteria
4. If brief is unclear: CB stops, escalates to TB (not user), waits
5. CB implements in as few iterations as possible
6. CB touches only explicitly allowed files
7. CB follows testing, documentation, commit, and versioning rules from brief
8. CB adds Implementation Notes section to brief
9. CB archives brief to `work/briefs/archive/`
10. CB stops (task complete)

**Note:** Brief should be approved by user before CB starts. If brief status is "Ready for Review", wait for user approval.

**Implementation Notes Format:**

```markdown
## Implementation Notes

**Executed:** YYYY-MM-DD HH:MM:SS
**Implemented By:** CODING_BUDDY

### What Was Implemented

[Summary of implementation]

### Deviations and Why

[Any deviations from brief and why they were necessary]

### Files Changed

- [List of files modified]

### Follow-up Risks or Suggestions

[Any risks or suggestions for future work]
```

**Success Criteria:**

- Brief requirements fully met
- No scope expansion
- All acceptance criteria satisfied
- Documentation updated (if required)
- Brief archived properly

### System Review (SYSTEM_BUDDY)

**CRITICAL: SYSTEM_BUDDY performs TWO types of reviews, both with equal importance:**

1. **System Health Review:** Focuses on code quality, architecture, dependencies, security, and overall system stability
2. **Context Integrity Review:** Focuses on documentation consistency, agent spec alignment, terminology coherence, context drift, and mental model health

**Both review types are core responsibilities of SYSTEM_BUDDY.** SYSTEM_BUDDY tracks last review dates for both types independently, proactively suggests both types, and performs both types of reviews. Neither review type is more important than the other - both are essential for system health.

**Trigger:**

- Manual invocation (periodic review) or specific issue investigation - user specifies review type
- **Proactive suggestion:** SYSTEM_BUDDY should suggest both review types independently when >7 days (weekly light) or >30 days (monthly deep) since last review of that type

**Proactive Suggestion Process:**

1. **For System Health Reviews:**

   - SYSTEM checks `work/findings/last_review_date.txt` file
   - Format: Single line `YYYY-MM-DD [A|B]` (date and cadence type)
   - If file doesn't exist: Check most recent findings file (`YYYY-MM-DD_system_health_review_findings.md`)
   - Extract date from filename, assume cadence `B` if unknown

2. **For Context Integrity Reviews:**

   - SYSTEM checks `work/findings/last_context_integrity_review_date.txt` file
   - Format: Single line `YYYY-MM-DD [A|B]` (date and cadence type)
   - If file doesn't exist: Check most recent findings file (`YYYY-MM-DD_context_integrity_review_findings.md`)
   - Extract date from filename, assume cadence `B` if unknown

3. Calculate time since last review for each type independently
4. If >7 days: Suggests weekly light review (Option A) for that type
5. If >30 days since last deep review: Suggests monthly deep review (Option B) for that type
6. User approves or declines each suggested review
7. If approved, proceed with review process below

**Review Process (after invocation/approval):**

1. SYSTEM determines review type (system health or context integrity) and cadence:
   - **Option A (Weekly light):** Quick check (1-2 hours)
     - System Health: Use `docs/prompts/system-health-review.txt`
     - Context Integrity: Use `docs/prompts/context-integrity-review.txt`
   - **Option B (Monthly deep):** Comprehensive analysis (half to full day)
     - System Health: Use `docs/prompts/system-health-review.txt`
     - Context Integrity: Use `docs/prompts/context-integrity-review.txt`
   - **Ad-hoc:** Focused on specific issue or area (user specifies type)
2. SYSTEM reviews requested scope
3. SYSTEM consults appropriate sources:
   - **System Health:** USER_GUIDE.md, SYSTEM_SUMMARY.md, codebase, dependencies, security posture
   - **Context Integrity:** USER_GUIDE.md, SYSTEM_SUMMARY.md, agent specs, documentation files, prompts, `docs/project-context/` (READ-ONLY reference for understanding project context, do not modify unless explicitly requested), observed behavior
4. SYSTEM documents observations (neutral, factual)
5. SYSTEM identifies issues, risks, and improvement opportunities
6. SYSTEM creates findings document following appropriate structure:
   - System Health: Follow structure in `docs/prompts/system-health-review.txt`
   - Context Integrity: Follow structure in `docs/prompts/context-integrity-review.txt`
7. SYSTEM exports findings to appropriate file:
   - System Health: `work/findings/YYYY-MM-DD_system_health_review_findings.md`
   - Context Integrity: `work/findings/YYYY-MM-DD_context_integrity_review_findings.md`
8. SYSTEM updates appropriate tracking file with review date and cadence type:
   - System Health: `work/findings/last_review_date.txt`
   - Context Integrity: `work/findings/last_context_integrity_review_date.txt`
   - File format: Single line `YYYY-MM-DD [A|B]` (e.g., `2026-01-10 A`)
   - Create file if it doesn't exist, overwrite if it exists
   - Also document review date in findings file itself (backup)
9. SYSTEM stops and waits for user/TB to review findings

**Findings Requirements:**

**For System Health Reviews (from system-health-review.txt):**

- Scope of Review (including cadence type: A, B, or Ad-hoc)
- Observations (neutral, factual - no solutions yet)
- Issues & Risks (with severity + likelihood)
- Improvement Opportunities (actionable, system-level, prioritized: Impact H/M/L, Effort S/M/L, Risk H/M/L)
- Automation Candidates (with preconditions + "do not automate yet" flags)
- Recommended Next Actions (for TB: briefs to create, for CB via TB: implementation targets, for operator: decisions needed)
- Organized into tranches: Quick wins (1-2h), Stability tranche (half day-2 days), Strategic tranche (bigger refactors)

**For Context Integrity Reviews (from context-integrity-review.txt):**

- Scope of Review (including cadence type: A, B, or Ad-hoc)
- Stable Truths (what is consistent and solid)
- Drift Signals (where things diverged)
- Inconsistencies & Contradictions (exact quotes or references that conflict)
- Missing or Implicit Context (decisions not documented, assumptions not stated)
- Risk Assessment (confusion, wrong decisions, agent misuse risks)
- Alignment Actions (prioritized: clarifications, decisions to surface, docs to update, terminology standardization)
- Questions to Resolve (unanswered questions, ambiguities)
- Classified findings (Drift, Contradiction, Missing Context, Implicit Decision, Outdated Assumption, Terminology Inconsistency, Weak Signal)
- Prioritized by Impact/Urgency/Confidence, organized into tranches

**Success Criteria:**

- Clear, actionable findings
- Issues prioritized by impact/effort/risk (system health) or impact/urgency/confidence (context integrity)
- Recommendations include context
- Findings can be used by TB to create briefs
- Last review date tracked separately for each review type for future proactive suggestions

### Context Clarification and Toolkit Guidance (CONTEXT_STEWARD)

**Trigger:** User needs help understanding the toolkit, their project, why things happen, or when system context is unclear

**Common scenario:** User sees code that looks wrong and wants to edit it manually - CONTEXT_STEWARD should check context first.

**CRITICAL: CONTEXT_STEWARD does NOT perform reviews.** CONTEXT_STEWARD explains, guides, and clarifies. If reviews are needed, CONTEXT_STEWARD routes to SYSTEM_BUDDY (who performs all reviews).

**Process:**

1. CONTEXT_STEWARD understands user intent and identifies what needs clarification
2. **If user sees code that looks wrong:** CONTEXT_STEWARD investigates context (briefs, docs, related code) to understand why it exists
3. CONTEXT_STEWARD clarifies context - explains what the system knows that the user doesn't
4. CONTEXT_STEWARD explains "why" things happen, not just "what" happens
5. **For "looks wrong" scenarios:** CONTEXT_STEWARD determines if code is actually wrong or just unfamiliar - prevents unnecessary edits
6. CONTEXT_STEWARD helps users understand and adapt the toolkit to their needs
7. CONTEXT_STEWARD provides clear, step-by-step guidance
8. If implementation needed: routes to TB (not directly to CB)
9. **If system review needed: routes to SYSTEM_BUDDY** (CONTEXT_STEWARD does NOT perform reviews)
10. CONTEXT_STEWARD can update documentation files and agent specs to clarify context or adapt the framework
11. CONTEXT_STEWARD NEVER writes code, never modifies project deliverables, and NEVER performs reviews

**Success Criteria:**

- User understands why things happen, not just what happens
- Context is clarified and transparent (no "black box" confusion)
- User understands how to use and adapt the toolkit
- User understands their project better
- Clear explanation of why approach is recommended
- Proper routing to other agents when needed
- No code written, no project deliverables modified

---

## Escalation Patterns

### CB Blocked by Brief

**Symptom:** CB cannot proceed because brief is unclear, contradictory, or missing information

**Process:**

1. CB stops implementation immediately
2. CB explains why brief is unclear:
   - What is ambiguous
   - What contradicts
   - What is missing
3. CB proposes alternative (if possible)
4. CB routes to TB for brief revision (not to user)
5. TB revises brief with clarifications
6. TB re-exports revised brief
7. CB continues with revised brief

**Never:**

- CB guesses missing intent
- CB partially implements with assumptions
- CB asks user directly (route through TB)

### SYSTEM Finds Issues

**Symptom:** SYSTEM_BUDDY identifies system problems or improvement opportunities

**Process:**

1. SYSTEM documents findings
2. Findings exported to `work/findings/YYYY-MM-DD_name_findings.md`
3. TB reviews findings
4. TB creates brief(s) for fixes/improvements
5. CB implements from brief(s)
6. CB updates SYSTEM_SUMMARY.md changelog

**Never:**

- SYSTEM implements fixes directly
- SYSTEM bypasses TB (always through TB → CB)
- SYSTEM creates briefs (that's TB's job)

### Context Steward Needs Implementation

**Symptom:** User asks CONTEXT_STEWARD to implement something

**Process:**

1. CONTEXT_STEWARD acknowledges request
2. CONTEXT_STEWARD routes to TB (not directly to CB)
3. TB creates brief
4. CB implements from brief
5. CONTEXT_STEWARD reviews results and communicates to user

**Never:**

- CONTEXT_STEWARD writes production code
- CONTEXT_STEWARD routes directly to CB
- CONTEXT_STEWARD creates briefs (that's TB's job)

---

## Handoff Artifacts

### Brief (TB → CB)

**Format:** Markdown file
**Location:** `work/briefs/YYYY-MM-DD_name_brief.md`
**Structure:**

- Context and goal
- Explicit requirements
- Non-goals
- Constraints and rules
- Acceptance criteria
- Standards or processes
- Testing expectations
- Documentation requirements
- Handoff note for CB

**Requirements:**

- Zero ambiguity
- All decisions explicit
- Scope clearly bounded
- Standalone (no external references needed)

### Findings (SYSTEM → TB)

**Format:** Markdown file
**Location:** `work/findings/YYYY-MM-DD_name_findings.md`
**Structure:**

- Scope of Review
- Observations
- Issues & Risks
- Improvement Opportunities
- Automation Candidates
- Recommended Next Actions

**Requirements:**

- Neutral, factual observations
- Prioritized recommendations
- Actionable proposals
- Clear context for TB

### Implementation Notes (CB → Brief)

**Format:** Section added to brief
**Location:** Same brief file (before archiving)
**Structure:**

- Execution timestamp
- What was implemented
- Deviations and why
- Files changed
- Follow-up risks or suggestions

**Requirements:**

- Honest about deviations
- Clear about what changed
- Useful for future reference

---

### Catch-Up Workflow (After Manual Edits)

**When user makes manual edits and needs to sync context:**

1. **User notifies THINKING_BUDDY:**

   - "I manually changed [X]. Can you create a catch-up brief?"
   - Describe what was changed and where

2. **THINKING_BUDDY creates catch-up brief:**

   - Documents the manual change
   - Identifies scope: what else needs updating (related code, docs, tests, etc.)
   - Creates brief: "Catch-up: [description] and ensure consistency"
   - Brief includes: what changed, why, what needs syncing

3. **User reviews catch-up brief:**

   - Approves if scope is correct
   - Requests changes if scope needs adjustment

4. **CODING_BUDDY executes catch-up:**

   - Finds all related references/code
   - Updates to match manual change
   - Updates documentation
   - Updates tests if needed
   - Updates SYSTEM_SUMMARY.md changelog
   - Ensures consistency across codebase

5. **Result:**
   - Manual change is documented
   - All related code/docs are updated
   - Context is consistent
   - SYSTEM_SUMMARY.md reflects the change

**Example: Variable rename catch-up**

- User: "I renamed `userEmail` to `email` in auth.js"
- TB: Creates brief to find all `userEmail` references and update
- CB: Finds all instances, updates consistently, updates docs/tests
- Context: Now consistent, agents know about the rename

## Additional Workflow Patterns

### Brief File Management

**Brief files (`work/briefs/YYYY-MM-DD_name_brief.md`):**

**Before implementation starts:**

- TB can revise brief (re-export with same or new name)
- User can request TB to revise brief
- Brief is "draft" until CB starts implementation

**After CB starts implementation:**

- Brief should NOT be edited (CB is working from it)
- If changes needed: TB creates revised brief with new name (e.g., add `_v2` suffix)
- CB compares old vs. new brief, adjusts implementation
- Old brief archived with note about revision

**After implementation complete:**

- Brief is read-only (historical record)
- CB adds Implementation Notes (final state)
- Brief archived to `work/briefs/archive/`

**Key principle:** Brief is a contract. Don't modify contract mid-execution. Revise and re-export instead.

### Agent Error Recovery

**If CODING_BUDDY implements incorrectly:**

1. **Detection:** User, SYSTEM_BUDDY, or CB itself notices the error
2. **Stop propagation:** Don't let wrong implementation become basis for new work
3. **Fix through workflow:**
   - TB creates brief to fix the incorrect implementation
   - CB implements fix (replacing wrong code)
   - SYSTEM_BUDDY reviews to ensure fix is correct
4. **Document in findings:** SYSTEM_BUDDY documents the error pattern to prevent recurrence

**If wrong implementation already spawned new briefs:**

- Identify all briefs/work based on wrong implementation
- TB revises or cancels affected briefs
- CB fixes root cause first
- Then proceed with corrected briefs

**Prevention:**

- Quality gates should catch errors before closure
- SYSTEM_BUDDY periodic reviews catch drift
- User review of CB output before accepting

### Parallel Work Coordination

**Multiple briefs in progress:**

- Each brief is independent
- CB implements one brief at a time (sequential by default)
- If briefs touch same files: TB must coordinate or sequence them
- Briefs should explicitly state if they conflict with other work

**Coordination rules:**

- TB should check for overlapping briefs before creating new one
- If briefs conflict: TB must sequence them or merge scope into single brief
- CB works on one brief until complete (no partial implementation across briefs)
- After brief complete, CB can pick up next brief

**For teams with multiple CB instances:**

- Briefs must be assigned to specific CB instance (via brief metadata)
- File-level coordination required (brief should list files it will modify)
- CB should check for other active briefs modifying same files before starting

---

## Communication Standards

### Be Explicit

- Never assume context
- State intent clearly
- Include "why" not just "what"
- Reference artifacts explicitly

### Include References

- Link to briefs: "See brief `2026-01-08_name_brief.md`"
- Link to findings: "See findings `2026-01-08_name_findings.md`"
- Link to documentation: "See USER_GUIDE.md section X"

### Acknowledge Boundaries

- "This is outside my role. Routing to [Agent]."
- "I need [Agent] to handle this. Should I create a brief/finding?"
- "This requires [Agent]'s expertise. Let me route this."

### Address Directly

- "CB, this needs code implementation. Should I create a brief?"
- "TB, this needs requirements clarified. Can you help?"
- "SYSTEM BUDDY, this workflow feels off. Can you review it?"
- "CONTEXT_STEWARD, I need to run this command. Is it safe?"

---

## Quality Gates

Quality gates are checkpoints that must pass before proceeding. If any gate fails, STOP AND ESCALATE.

### THINKING_BUDDY Quality Gates

- Intent is clear (no major ambiguities)
- Scope is defined
- Constraints are explicit
- Non-goals are stated
- Success criteria are measurable
- Brief is complete and standalone

### CODING_BUDDY Quality Gates

- Brief is complete and unambiguous
- Requirements don't contradict each other
- Technical feasibility is confirmed
- All dependencies are identified
- Acceptance criteria are clear

### SYSTEM_BUDDY Quality Gates

- Scope of analysis is clear
- Findings are actionable
- Recommendations include context
- Findings reference relevant artifacts
- Prioritization is explicit

### CONTEXT_STEWARD Quality Gates

- User intent is understood
- Guidance is clear and actionable
- Proper routing to other agents when needed
- No implementation work attempted

---

## Operational Best Practices

### Agent Instance Management

**Keep separate agent instances for optimal performance:**

- **THINKING_BUDDY:** Dedicated conversation for brief creation
- **CODING_BUDDY:** Dedicated conversation for implementation
- **SYSTEM_BUDDY:** Dedicated conversation for system reviews
- **CONTEXT_STEWARD:** Dedicated conversation for toolkit guidance, project understanding, and context clarification

**Why separate instances:**

- Maintains role fidelity over long conversations
- Prevents role boundary drift
- Enables clean handoffs between agents
- Easier to refresh context when needed

### Context Refresh

**Refresh agent context regularly to prevent drift:**

**Refresh when:**

- Conversation gets long (>50-100 messages)
- Agent violates role boundaries
- Switching between different work types
- Starting a new work session
- Agent seems confused about its role

**How to refresh:**

1. Re-invoke the agent's start prompt (`docs/prompts/system-[agent-name].txt`)
2. Reference the agent specification (`docs/agents/[AGENT_NAME].md`)
3. If drift persists, start fresh conversation with clean initialization

**Proactive refresh schedule:**

- Daily: Refresh at start of work session
- Per task: Refresh before new brief/implementation/review cycle
- On drift: Immediate refresh when boundary violations occur

**Signs of agent drift:**

- Agent suggests actions outside its role
- Agent tries to do everything (loses role focus)
- Agent bypasses workflow (e.g., CB implementing without brief)
- Agent mixes responsibilities between roles

See `README.md` Best Practices section for detailed guidance.

---

## Documentation Update Rules

**⚠️ CRITICAL: For comprehensive documentation standards, maintenance guidelines, formatting rules, and quality standards, see:**
**`docs/DOCUMENTATION_STANDARDS.md`**

This section provides quick reference for workflow-specific documentation updates. The comprehensive standards document covers:

- Document header standards (version numbering, date format)
- Agent documentation responsibilities
- Update triggers and processes by document type
- Quality standards and formatting rules
- Cross-reference management
- Review and validation processes

### Quick Reference: Who Updates What

**CODING_BUDDY (Primary Documentation Maintainer):**

- `docs/system/SYSTEM_SUMMARY.md` - MANDATORY after implementation (add changelog entry)
- `docs/USER_GUIDE.md` - When user-facing behavior changes
- Root `README.md` - When framework structure changes
- Code-level documentation - When brief requires

**THINKING_BUDDY:**

- Briefs (documentation artifacts)
- `docs/USER_GUIDE.md` - When introducing new workflows (in coordination with CB)
- Agent specs - When role boundaries change significantly

**CONTEXT_STEWARD:**

- Framework documentation - When clarifying context or adapting framework
- Agent specs - When clarifying roles or adapting framework

**SYSTEM_BUDDY:**

- Creates findings about documentation issues (does NOT update directly)
- Validates documentation freshness during context integrity reviews

### Quick Reference: Update Triggers

**After Implementation (CB):**

- System behavior changed → Update `SYSTEM_SUMMARY.md` changelog
- User-facing behavior changed → Update `USER_GUIDE.md`
- Framework structure changed → Update `README.md`

**During Brief Creation (TB):**

- New workflow → Plan `USER_GUIDE.md` updates in brief
- Agent role changes → Plan agent spec updates in brief

**MANDATORY: Always update version and date in document header when updating any documentation.**

---

## Notes

- Workflows are explicit, not implicit
- Handoffs use structured artifacts
- Escalation always includes explanation and proposed path
- Quality gates prevent proceeding with ambiguity
- Documentation updates are mandatory, not optional
