# Context Management Bootstrap Kit

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** Reusable context management framework for AI-assisted development environments

---

## Overview

This bootstrap kit provides a complete context management framework extracted from proven agent-based development workflows. It defines agent roles, documentation contracts, workflow patterns, and system prompts that create a sustainable, maintainable AI-assisted development environment.

## What This Kit Provides

- **Four core agent roles** with explicit boundaries and responsibilities
- **Documentation contracts** that ensure context stays current and accurate
- **Project context folder** for storing project-specific domain knowledge, business rules, and requirements
- **Workflow patterns** for agent collaboration and handoffs
- **System prompts** that enforce role fidelity and prevent scope drift
- **Quality assurance system** with mandatory quality gates and validation checkpoints
- **Maintenance rules** that keep documentation aligned with reality
- **Catch-up process** for syncing manual edits with agents (flexible workflow)
- **Project brief template** for structured intent capture

## ⚠️ Context Drift and Manual Editing

### The Reality

**You can manually edit code, but you are responsible for context drift.**

Manual edits create a gap between what you know and what agents know. This gap (context drift) breaks the context management system if not addressed.

**The Process:**

- **Before manual edits:** If something looks wrong, consult CONTEXT_STEWARD first to understand context
- Manual edits are OK for small, isolated changes (after checking context if it looks wrong)
- After manual edits: Request catch-up brief to sync context
- Briefs ensure related code/docs are updated
- Don't let manual edits accumulate

**Your Responsibility:**

- **Check context first:** If code looks wrong, ask CONTEXT_STEWARD why it exists before editing
- You're responsible for context drift when you manually edit
- Always request catch-up brief after manual edits
- Use briefs for features and significant changes
- Balance: Speed when appropriate, sync to maintain context

**See `docs/RULES.md` for complete rules, risk assessment, and catch-up processes.**

---

## Critical Distinction

**IMPORTANT:** This bootstrap kit is a **meta-framework** that provides structure for documenting YOUR ACTUAL PROJECT.

The templates (`USER_GUIDE.md` and `SYSTEM_SUMMARY.md`) are designed to document YOUR PRODUCT/SYSTEM, not the bootstrap kit itself.

**Example:** When building a webshop:

- `USER_GUIDE.md` describes how customers use the webshop (browsing, shopping cart, checkout)
- `SYSTEM_SUMMARY.md` describes the webshop's architecture (frontend, backend, database, payment integration)

These documents do NOT describe the context management framework or agent roles—they document your actual project that uses the framework.

The framework itself is documented in:

- `docs/agents/` - Agent specifications (framework components)
- `docs/WORKFLOW.md` - Workflow patterns (framework processes)
- `docs/prompts/` - System prompts (framework configuration)

**Always replace `[YOUR PROJECT NAME]` placeholders with your actual project name and customize all example content.**

## Project Context Folder

**IMPORTANT:** Store all project-specific context in the `docs/project-context/` folder.

This dedicated folder is where you store project-specific domain knowledge, business rules, requirements, specifications, and any other contextual information that agents need to understand your project.

### ⚠️ READ-ONLY CONTEXT (Critical)

**This folder is READ-ONLY by default. Agents will NOT maintain or update files in this folder unless explicitly asked.**

- **Agents read from this folder** to understand project context, business rules, domain knowledge, and requirements
- **Agents do NOT automatically update** files in this folder
- **If you want agents to update project context**, you must explicitly request it in a brief or task
- **This is reference material** - like external documentation that agents consult but don't modify

Files in `docs/project-context/` are treated as authoritative reference sources, similar to third-party documentation. Agents use them to inform decisions and understand constraints, but they remain static unless you explicitly request updates.

### What to Store Here

- **Domain requirements and business rules** - Business logic, domain-specific terminology, compliance requirements
- **Project specifications** - API contracts, integration requirements, third-party service documentation
- **Business context** - Target users, business model, success metrics, roadmap information
- **Reference materials** - Requirements documents, design specifications, stakeholder notes (as PDF, DOCX, or Markdown)

### File Formats

- **Preferred:** Markdown (`.md`) files - Agents can read these directly
- **Supported:** PDF (`.pdf`) and DOCX (`.docx`) files - Agents can extract text from these formats
- **Organization:** Organize files by topic (e.g., `domain-requirements.md`, `api-specifications.md`, `integration-docs.pdf`)

### How Agents Use This Folder

All agents (THINKING_BUDDY, CODING_BUDDY, SYSTEM_BUDDY, CONTEXT_STEWARD) treat files in `docs/project-context/` as **read-only reference sources**. When agents need to understand:

- Business rules or domain constraints → They reference files in this folder (read-only)
- Integration requirements → They check project-context files (read-only)
- Domain terminology or concepts → They consult this folder (read-only)
- Project-specific requirements → They use this as source of truth (read-only)

**Example:** When THINKING_BUDDY creates a brief for a new feature, it should check `docs/project-context/` for business rules that might constrain the implementation. When CODING_BUDDY implements, it should verify compliance with domain requirements stored here. Neither agent will modify these files unless explicitly requested.

**If business rules or domain requirements change:**

- You (the user) manually update files in `docs/project-context/` OR
- Explicitly request an agent (via brief or task) to update specific files in this folder
- Agents will not automatically detect and update stale project context

The example file `docs/project-context/domain-requirements-EXAMPLE.md` is a placeholder that can be safely deleted. This folder is for storing all your project-specific context - domain knowledge, business rules, requirements, API specifications, etc. Create your own project-context files as needed. Files with "-EXAMPLE" suffix are automatically ignored by agents.

## Quick Start

1. **Read the Rules (IMPORTANT):**

   - **Read `docs/RULES.md` first** - Understand context drift and the catch-up process
   - Understand: You can manually edit, but must sync with agents afterward
   - Learn the catch-up workflow for maintaining context consistency

2. **Review the framework:**

   - **Framework documentation** (how the bootstrap kit works):
     - Review `docs/WORKFLOW.md` for process patterns
     - Review `docs/QUALITY_STANDARDS.md` for quality expectations
     - Bookmark `docs/TROUBLESHOOTING.md` for when issues arise
     - Review `docs/agents/` for agent specifications
   - **Project documentation templates** (currently contain example content, will be customized for YOUR project):
     - `docs/USER_GUIDE.md` - Template for documenting how users interact with YOUR system (currently has example/placeholder content - will be customized)
     - `docs/system/SYSTEM_SUMMARY.md` - Template for documenting YOUR system's architecture and technical details (currently has example/placeholder content - will be customized)
     - **Note:** These templates currently contain example content. After customization, agents will maintain these documents with information about YOUR project. They do NOT describe how the bootstrap kit works.
   - **Populate `docs/project-context/`** with your project-specific domain knowledge (see SETUP.md)

3. **Configure agents:**

   - Copy system prompts from `docs/prompts/` to your AI assistant
   - Customize agent specs in `docs/agents/` for your needs
   - Set up start prompts for agent initialization
   - **Recommended:** Keep separate agent instances (one conversation per agent: THINKING_BUDDY, CODING_BUDDY, SYSTEM_BUDDY, CONTEXT_STEWARD)
   - **Recommended:** Refresh agent context regularly (daily or per task) by re-invoking start prompts to maintain role fidelity

4. **Customize templates:**

   - **Option A (Recommended):** Use THINKING_BUDDY with `docs/prompts/setup-thinking-buddy.txt` for automated customization
   - **Option B:** Manually customize templates (see SETUP.md for details)
   - Replace all `[YOUR PROJECT NAME]` placeholders
   - Replace example content with your actual project details

5. **Establish workflows:**

   - Work directories are already created (no manual setup needed):
     - `work/briefs/` - Execution briefs (THINKING_BUDDY → CODING_BUDDY)
     - `work/findings/` - System findings (SYSTEM_BUDDY → THINKING_BUDDY)
     - `work/briefs/archive/` - Archived briefs after implementation
   - Verify `docs/system/SYSTEM_SUMMARY.md` template is customized (if using Option B)
   - Verify templates are customized (if using Option A)
   - Create your own project-context files (see `docs/project-context/README.md`)

6. **Begin using:**
   - Use Thinking Buddy to create briefs
   - Use Coding Buddy to implement from briefs (let them code, even if wrong - they'll fix it)
   - Use System Buddy for periodic reviews (System Buddy will proactively suggest weekly/monthly reviews)
   - Use Context Steward for operational guidance
   - **Remember:** Manual edits are OK, but sync with agents afterward via catch-up briefs

---

## Best Practices

### Keep Separate Agent Instances

**This framework works best when you keep 4 separate agent conversations open:**

1. **THINKING_BUDDY** - One dedicated conversation for requirement clarification and brief creation
2. **CODING_BUDDY** - One dedicated conversation for implementation and code work
3. **SYSTEM_BUDDY** - One dedicated conversation for system reviews and findings
4. **CONTEXT_STEWARD** - One dedicated conversation for toolkit guidance, project understanding, and context clarification

**Why separate instances matter:**

- **Role fidelity:** Each agent maintains its role boundaries more effectively
- **Context clarity:** Each conversation stays focused on that agent's domain
- **Reduced confusion:** Agents don't mix responsibilities or drift between roles
- **Better workflow:** Clean handoffs between agents (brief → implementation → review)

**If you must use a single conversation:**

- Clearly identify which agent role you're invoking
- Use the agent's start prompt to re-establish role boundaries
- Be explicit about role transitions ("Now switching to CODING_BUDDY role...")

### Refresh Context Regularly

**If you notice agent drift (agent acting outside role boundaries), refresh context:**

**Signs of agent drift:**

- Agent suggests actions outside its role (e.g., CODING_BUDDY creating briefs, THINKING_BUDDY writing code)
- Agent forgets role boundaries and tries to be "helpful" by doing everything
- Agent mixes responsibilities between different roles
- Agent bypasses workflow (e.g., CB trying to implement without brief)

**How to refresh context:**

1. **Re-invoke the agent's start prompt:**

   - Copy the relevant prompt from `docs/prompts/system-[agent-name].txt`
   - Paste it as a new message to reset role boundaries
   - Agent will acknowledge with "READY" and reset to proper role

2. **Reference the agent specification:**

   - Point agent to `docs/agents/[AGENT_NAME].md`
   - Remind agent of its specific role and boundaries
   - Clarify what it should and should NOT do

3. **If drift persists:**
   - Start a fresh conversation with the agent
   - Use the start prompt to initialize cleanly
   - Copy relevant context (briefs, findings) as needed

**When to refresh:**

- After long conversations (>50-100 messages)
- When you notice role boundary violations
- When switching between different types of work
- At the start of each new session/day
- When agent seems confused about its role

**Proactive refresh schedule (recommended):**

- **Daily:** Re-invoke start prompts at the beginning of work session
- **Per task:** Refresh before starting a new brief/implementation/review cycle
- **On drift:** Immediate refresh when you notice boundary violations

**Benefits of regular refresh:**

- Maintains role fidelity over long conversations
- Prevents gradual drift into "helpful" general assistant mode
- Keeps workflow clean and predictable
- Ensures agents stay within their specified boundaries

---

## Structure

```
context-management-bootstrap/
├── README.md                    # This file
├── SETUP.md                     # Step-by-step setup guide
├── work/                        # Work directories (pre-created)
│   ├── briefs/                 # Active execution briefs
│   │   └── archive/            # Archived briefs after implementation
│   └── findings/               # System analysis findings
└── docs/
    ├── RULES.md                # ⚠️ IMPORTANT: Rules and context drift management
    ├── CATCHUP_GUIDE.md        # Quick reference for catch-up process
    ├── TROUBLESHOOTING.md      # Common issues and solutions
    ├── USER_GUIDE.md           # User-facing guide template
    ├── system/
    │   └── SYSTEM_SUMMARY.md   # System documentation template
    ├── project-context/        # READ-ONLY project-specific context and domain knowledge
    │   ├── README.md           # READ-ONLY folder explanation
    │   └── domain-requirements-EXAMPLE.md  # ⚠️ EXAMPLE: Placeholder file that can be safely deleted - create your own project-context files
    ├── WORKFLOW.md             # Workflow patterns
    ├── DECISIONS.md            # Decision log template
    ├── QUALITY_STANDARDS.md    # Quality standards and validation criteria
    ├── agents/                 # Agent specifications
    │   ├── THINKING_BUDDY.md
    │   ├── CODING_BUDDY.md
    │   ├── SYSTEM_BUDDY.md
    │   └── CONTEXT_STEWARD.md
    ├── prompts/                # System prompts (plain text)
    │   ├── system-thinking-buddy.txt
    │   ├── system-coding-buddy.txt
    │   ├── system-system-buddy.txt
    │   ├── system-context-steward.txt
    │   ├── setup-thinking-buddy.txt
    │   └── system-health-review.txt
    └── briefs/                 # Templates
        ├── project-brief-template.md
        └── quality-checklist-template.md
```

## Key Concepts

### Agent Roles

- **THINKING_BUDDY**: Clarifies intent, creates execution briefs, owns requirements
- **CODING_BUDDY**: Implements from briefs, owns code quality, enforces scope, validates quality gates
- **SYSTEM_BUDDY**: Observes system health, identifies improvements, creates findings, proactively suggests system reviews
- **CONTEXT_STEWARD**: Guides toolkit usage, clarifies project context, explains why things happen, helps adapt framework to your needs (never writes code, can update documentation)

### Why Two Agents? (TB and CB)

**This might look like overkill, but the separation has a clear purpose:**

**The Problem with One Agent:**

- Single agent mixes requirements and implementation thinking
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

1. **Role Separation and Responsibility:**

   - TB owns intent, scope, and requirements (captured in brief)
   - CB owns implementation quality and execution (from brief)
   - Clear authority transfer: brief is the contract between roles
   - Prevents scope creep and boundary blurring
   - Each role has clear ownership and accountability

2. **User Review and Final Approval:**

   - Brief gives user opportunity to review before execution
   - User can approve, request changes, or cancel before CB starts
   - Final checkpoint before implementation begins
   - User has explicit "final say" on what will be built
   - Prevents misunderstandings and unwanted features

3. **Documentation and History:**
   - Brief documents the change/feature request permanently
   - Implementation Notes (added by CB) document what was actually built
   - Creates audit trail: why something was built, what was built, what changed
   - Historical record for future reference and learning
   - Enables understanding of system evolution over time

### Quality Assurance

- **Mandatory Quality Gates**: CODING_BUDDY must pass all quality gates before closure
- **Quality Standards**: Defined in `docs/QUALITY_STANDARDS.md` (code quality, testing, documentation)
- **Validation Checkpoints**: Pre-implementation, during implementation, and pre-completion gates
- **Acceptance Criteria Verification**: All criteria must be testable and verified
- **Quality Checklist**: Template available in `docs/briefs/quality-checklist-template.md`

### Document Contracts

- **USER_GUIDE.md**: How to use the system (updated when behavior changes)
- **SYSTEM_SUMMARY.md**: Living documentation with changelog (updated after every change)
- **Agent Specs**: Role definitions and boundaries (updated when behavior changes)
- **System Prompts**: Prompt text that enforces roles (updated when roles change)

### Workflow Patterns

- **TB → CB**: Brief (`work/briefs/YYYY-MM-DD_name_brief.md`)
- **SYSTEM → TB**: Findings (`work/findings/YYYY-MM-DD_name_findings.md`)
- **Escalation**: Always explain why, propose path forward
- **Handoffs**: Use structured artifacts, include sufficient context

## Tool-Agnostic Design

This kit is designed to work with any AI assistant tool (Cursor, Claude Code, ChatGPT, etc.). It focuses on:

- Role definitions and boundaries
- Documentation structure and contracts
- Workflow patterns and handoffs
- Context management principles

It does NOT prescribe:

- Specific tools or platforms
- Implementation technologies
- Project structures
- File organization beyond documentation

## Maintenance

See documentation update rules in `docs/WORKFLOW.md` for:

- When USER_GUIDE is updated
- When SYSTEM_SUMMARY is updated
- When agent specs are updated
- When system prompts are updated
- Who validates freshness

## License

This bootstrap kit is provided as-is. Adapt it to your needs.
