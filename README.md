# Context Management Bootstrap Kit

**Version:** 1.6  
**Last Updated:** 2026-01-10  
**Purpose:** Reusable context management framework for AI-assisted development environments

> **🚀 Multi-agent system with shared knowledge** - Four specialized AI agents coordinate through structured workflows, sharing a persistent knowledge base to maintain context consistency and reduce drift.

---

## What Is This?

The **Context Management Bootstrap Kit** is a framework that helps you work effectively with AI coding assistants by keeping everyone (you and your AI agents) on the same page. Instead of struggling with context drift, outdated documentation, and agents that forget what they're supposed to do, this kit gives you a structured system where everything stays in sync.

**In simple terms:** It's a set of rules, workflows, and templates that turn your AI assistant into a reliable development partner. You configure four specialized "agent roles" in your AI assistant (like [Cursor](https://cursor.com/downloads)) - think of them as separate team members for planning, coding, system reviews, and guidance. Each agent has a specific system prompt that defines its role and boundaries. They share clear workflows for how they work together, and automatic documentation that stays up-to-date with your codebase.

**What makes it work:** Agents share a common knowledge base (documentation, project context) that they all read from and write to. This creates a "collective memory" - when one agent learns something, others can access it. They coordinate through structured handoffs (briefs, findings) rather than direct communication, creating a distributed system where each agent has a specialized role but the whole system stays synchronized.

## How Do You Use It?

**The basic workflow is simple:**

1. **Set up the framework** (one-time):

   - Copy the kit and configure your AI agents with the provided prompts
   - **Customize templates:** Use THINKING_BUDDY with `docs/prompts/setup-thinking-buddy.txt` to populate `USER_GUIDE.md` and `SYSTEM_SUMMARY.md` with your project information. TB will interview you and create a brief for CODING_BUDDY to execute the customization. This basically shows you how the framework works in practice.
   - Populate `docs/project-context/` with your domain knowledge and business rules

2. **Start working on your project:** Tell THINKING_BUDDY how you want to start. They'll ask clarifying questions and create a detailed "brief" of the feature/change (executable specification) for you to review.

   > **Note:** The system doesn't have much context yet and isn't sure which direction you want to go. Give it a few tries—it will learn. Trust it and remember: more context → better results.

3. **Review and approve:** You review the brief before any code is written. This is your checkpoint to ensure everything is correct.

4. **Implementation:** CODING_BUDDY takes the approved brief and implements it, following quality standards and updating documentation automatically.

5. **Ongoing maintenance:**
   - **SYSTEM_BUDDY** proactively reviews your system health, context integrity and suggests improvements
   - **CONTEXT_STEWARD** answers your questions about the system, workflows, and agent behavior - ask instead of reading all docs. Helps you understand why things happen and adapt the framework to your needs.

**That's it!** The framework handles the coordination, ensures quality gates are met, keeps documentation current, and prevents scope creep. You just provide direction and review checkpoints.

**Manual edits?** They're fine! Just request a "catch-up brief" afterward to sync everything back up. The system is flexible, not rigid.

---

## Quick Start

1. **Read the essential rules first** (`docs/RULES.md`) - Understand how manual edits work and the catch-up process. This is important but not complicated.

2. **Run setup** (`SETUP.md`) - Copy prompts to your AI assistant, customize templates, and populate project context.

3. **Start using it** - Ask THINKING_BUDDY to create a brief for your first feature, review it, then have CODING_BUDDY implement it.

4. **Get help and maintain quality** - Ask CONTEXT_STEWARD questions about workflows, agent behavior, or how to adapt the framework. SYSTEM_BUDDY proactively reviews your system health and context integrity, suggesting improvements when needed.

That's the basics! For detailed setup instructions, see `SETUP.md`. For troubleshooting, see `docs/TROUBLESHOOTING.md`.

---

## What This Kit Provides

- **Four specialized agent roles** (THINKING_BUDDY, CODING_BUDDY, SYSTEM_BUDDY, CONTEXT_STEWARD) with clear boundaries and responsibilities
- **Shared knowledge architecture** - Documentation and project context that all agents read from and maintain
- **Structured workflows** - Clear handoff patterns (briefs, findings) that prevent scope creep and maintain quality
- **Self-updating documentation** - Living documentation system that automatically stays in sync with your codebase
- **Quality gates and validation** - Mandatory checkpoints ensuring consistent, maintainable implementations
- **Project context management** - Dedicated READ-ONLY folder for domain knowledge, business rules, and requirements
- **Context synchronization** - Catch-up process for syncing manual edits back into the system
- **Proactive monitoring** - Automated health checks and context integrity reviews

---

## Important Details

### ⚠️ Manual Editing and Context Drift

**You can manually edit code, but you need to sync with agents afterward.** Manual edits create a gap between what you know and what agents know (called "context drift").

**The simple rule:** If something looks wrong, ask CONTEXT_STEWARD to explain it first. After manual edits, request a "catch-up brief" to sync everything back up. For detailed rules and best practices, see `docs/RULES.md`.

---

### Understanding Templates vs. Framework

**Important:** This bootstrap kit is a **meta-framework** for documenting YOUR project. The templates (`USER_GUIDE.md` and `SYSTEM_SUMMARY.md`) document YOUR product, not the framework itself.

**Example:** Building a webshop? The templates describe how customers use your webshop and its architecture. The framework documentation (in `docs/agents/`, `docs/WORKFLOW.md`, etc.) describes how the agent system works. Always replace `[YOUR PROJECT NAME]` placeholders with your actual project name.

### Project Context Folder

Store all project-specific domain knowledge, business rules, and requirements in `docs/project-context/`. **This folder is READ-ONLY by default** - agents read from it but won't automatically update it unless you explicitly ask. You can store Markdown, PDF, or DOCX files organized by topic. See `docs/project-context/README.md` for details.

---

## Best Practices

### Keep Separate Agent Instances

**This framework works best when you keep 4 separate agent conversations open:**

1. **THINKING_BUDDY** - One dedicated conversation for requirement clarification and brief creation
2. **CODING_BUDDY** - One dedicated conversation for implementation and code work
3. **SYSTEM_BUDDY** - One dedicated conversation for system health reviews, context integrity reviews, and findings
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
    ├── DOCUMENTATION_STANDARDS.md  # Documentation standards and maintenance guidelines
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
    │   ├── system-health-review.txt
    │   └── context-integrity-review.txt
    └── briefs/                 # Templates
        ├── project-brief-template.md
        └── quality-checklist-template.md
```

## Key Concepts

### Agent Roles

- **THINKING_BUDDY**: Clarifies intent, creates execution briefs, **owns feature requirements**
- **CODING_BUDDY**: Implements from briefs, **owns code and documentation maintenance**, enforces scope, validates quality gates
- **SYSTEM_BUDDY**: **Owns system health and performs ALL reviews** - observes, analyzes, identifies improvements, creates findings. Performs two equally important review types: (1) System Health Reviews (code quality, architecture, dependencies, security), and (2) Context Integrity Reviews (documentation consistency, agent spec alignment, terminology coherence). Tracks last review dates for both types independently and proactively suggests both types.
- **CONTEXT_STEWARD**: **Owns context health (guidance only)** - guides toolkit usage, clarifies project context, explains why things happen, helps adapt framework to your needs. Can update documentation and agent specs to clarify context, but does NOT perform reviews (routes review requests to SYSTEM_BUDDY). Never writes code, focuses on explanation and guidance.

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

- **Owns:** Feature requirements (intent, requirements, scope, decisions)
- **Focus:** "What" and "Why" - understanding the problem completely
- **Output:** Brief (executable specification)
- **Stops:** After brief is created and approved

**CODING_BUDDY (CB):**

- **Owns:** Code and documentation maintenance (implementation quality, code execution, keeping docs current)
- **Focus:** "How" - executing from the brief
- **Input:** Brief (the contract)
- **Stops:** After implementation is complete

**Why This Works:**

1. **Cognitive Separation:** Different mental models - TB thinks about problems, CB thinks about solutions
2. **Quality Gate:** Brief serves as mandatory checkpoint - user reviews before execution
3. **Scope Control:** CB can't expand scope (it's not in the brief) - prevents feature creep
4. **Accountability:** Clear ownership - TB owns feature requirements, CB owns code and documentation maintenance
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

- **USER_GUIDE.md**: Documents how the system you're building (not this kit) works from a user perspective - describes and safeguards user-facing behavior and workflows (updated when behavior changes)
- **SYSTEM_SUMMARY.md**: Living documentation that tracks system changes and system-level decisions (updated after every change, references briefs for implementation details, documents architectural decisions)
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
