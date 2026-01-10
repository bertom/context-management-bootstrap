# Setup Guide

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** Step-by-step setup instructions for the context management bootstrap kit

---

## Prerequisites

- An AI assistant tool (This kit is optimized for Cursor)
- A project repository or workspace
- Basic familiarity with markdown and documentation
- **Willingness to let agents write code** (critical mindset shift - see RULES.md)

---

## ⚠️ IMPORTANT: Read the Rules First

**Before proceeding, read `docs/RULES.md` completely.**

The framework balances flexibility with context management:

- **You can manually edit code** (for small, isolated changes)
- **Agents maintain system-wide context** (documentation, related code, tests)
- **Manual edits create context drift** (gap between what you know and what agents know)
- **Catch-up process syncs manual changes** (brief documents change, agents update related code/docs)

**Key understanding:**

- Manual edits are OK, but you're responsible for context drift
- After manual edits, request catch-up brief to sync context
- Use briefs for features and significant changes
- Balance: Speed when appropriate, sync to maintain context

**If you're not willing to sync manual edits with agents, context drift will accumulate and break the system.**

---

## Step 1: Copy Files to Your Project

Copy the entire `context-management-bootstrap/` folder to your project, or copy its contents to your existing documentation structure.

**Option A: Standalone folder**

```bash
cp -r context-management-bootstrap /path/to/your/project/
cd /path/to/your/project/context-management-bootstrap
```

**Option B: Integrate into existing docs**

```bash
# Copy docs structure
cp -r context-management-bootstrap/docs/* /path/to/your/project/docs/

# Copy prompts to appropriate location
cp -r context-management-bootstrap/docs/prompts/* /path/to/your/project/docs/prompts/
```

---

## Step 2: Verify Work Directories and Project Context Folder

**The work directories are already created** when you copy the bootstrap kit. These directories are for:

- `work/briefs/` - Active execution briefs (THINKING_BUDDY creates, CODING_BUDDY archives)
- `work/briefs/archive/` - Completed briefs after implementation
- `work/findings/` - System analysis findings (SYSTEM_BUDDY creates)
- `work/findings/last_review_date.txt` - Tracking file for last system health review (created automatically by SYSTEM_BUDDY after first review, format: `YYYY-MM-DD [A|B]`)

**The project context folder (`docs/project-context/`) is also already created** when you copy the bootstrap kit. This folder is where you store project-specific domain knowledge, business rules, and requirements.

No manual directory creation is needed - the bootstrap kit includes all required directories.

### Populate Project Context Folder

**IMPORTANT:** The `docs/project-context/` folder contains READ-ONLY project-specific context that agents will reference. You should:

1. **Review the README:**

   - `docs/project-context/README.md` - Explains that this folder is READ-ONLY for agents
   - Agents will NOT automatically maintain or update files here unless explicitly asked

2. **Review the example file and create your own:**

   - `docs/project-context/domain-requirements-EXAMPLE.md` - Example template following the webshop placeholder pattern
   - **⚠️ CRITICAL:** This file has "-EXAMPLE" suffix and contains EXAMPLE/PLACEHOLDER content about "Acme Webshop" - this is NOT real project context
   - **The "-EXAMPLE" suffix makes it clear this is a template** - agents will ignore files with this suffix
   - **Create your own file** (e.g., `domain-requirements.md`) with your actual project's domain knowledge, business rules, and requirements
   - You can delete the example file once you've created your own, or keep it as a reference
   - Agents should NOT treat "Acme Webshop" or any placeholder content as real project context

3. **Add your project-specific context files:**

   - **Domain requirements and business rules** (e.g., `domain-requirements.md`, `business-rules.md`)
   - **API specifications** (e.g., `api-contracts.md`, `integration-specs.md`)
   - **Third-party documentation** (e.g., `payment-gateway-spec.pdf`, `shipping-api.docx`)
   - **Business context** (e.g., `user-personas.md`, `success-metrics.md`, `roadmap.md`)

4. **File format guidelines:**

   - **Preferred:** Markdown (`.md`) files - Agents can read these directly
   - **Supported:** PDF (`.pdf`) and DOCX (`.docx`) files - Agents can extract text from these
   - **Organization:** Use descriptive filenames and organize by topic

5. **Content guidelines:**
   - Store project-specific information only (not framework documentation)
   - Keep files focused and well-organized
   - **You maintain these files** - Agents won't automatically update them
   - Update files manually when business rules or requirements change
   - If you want agents to update files here, explicitly request it in a brief or task
   - Include version and date headers (see example file)

**Note:** Agents will read files in `docs/project-context/` when they need to understand business rules, domain constraints, integration requirements, or project-specific terminology. However, agents treat this folder as READ-ONLY and will NOT maintain or update files unless explicitly asked. Make sure this folder contains all relevant project context and keep it current manually.

---

## Step 3: Initialize Core Documents

### Option A: Automated Customization (Recommended)

Use THINKING_BUDDY to automatically customize the templates through a guided interview:

1. **Templates are already in final locations:**

   - `docs/system/SYSTEM_SUMMARY.md` - Already in correct location (no copy needed)
   - `docs/USER_GUIDE.md` - Already in correct location

   If you need to move files to a different structure, do so before starting the customization process.

2. **Start THINKING_BUDDY with the setup prompt:**

   **Option 1:** Copy the setup prompt from `docs/prompts/setup-thinking-buddy.txt` and paste it as your first message to THINKING_BUDDY

   **Option 2:** Start a new conversation with THINKING_BUDDY using the regular start prompt (`docs/prompts/system-thinking-buddy.txt`), then say:

   "Help me customize the bootstrap kit templates for my project. I need to populate USER_GUIDE.md and SYSTEM_SUMMARY.md with information about [project name]."

   THINKING_BUDDY will recognize this as a template customization task and proceed with the interview.

3. **Answer THINKING_BUDDY's questions:**

   - Project name
   - Project purpose and functionality
   - Target users and roles
   - Main features
   - Technology stack
   - Architecture (if known)
   - Key workflows

4. **Review the brief:**

   - THINKING_BUDDY will create a brief at `work/briefs/YYYY-MM-DD_template-customization_brief.md`
   - Review the brief to ensure it captures your project correctly

5. **Execute customization:**
   - Hand the brief to CODING_BUDDY
   - CODING_BUDDY will update both USER_GUIDE.md and SYSTEM_SUMMARY.md based on the brief

**Benefits:**

- Systematic information gathering
- No manual find/replace errors
- Ensures all placeholders are addressed
- Creates a record of your project information in the brief

### Option B: Manual Customization

If you prefer to customize manually:

**Initialize SYSTEM_SUMMARY.md:**

The template is already at `docs/system/SYSTEM_SUMMARY.md`. Edit it directly:

```bash
# Edit docs/system/SYSTEM_SUMMARY.md with your project name and details
```

**Note:** This is the **only time** manual editing of these files is allowed. After customization, all changes must go through briefs.

**CRITICAL:** Replace ALL placeholder content:

- Replace `[YOUR PROJECT NAME]` with your actual project name (e.g., "Acme Webshop")
- Replace all example content (webshop examples) with YOUR actual project details
- This document describes YOUR PROJECT, not the bootstrap kit itself
- Remove the template warning once customized

Update the "System Overview" section with:

- Your project name
- Your system's purpose (what your project does, not the framework)
- Your core components (your application's components, not agent roles)

**Customize USER_GUIDE.md:**

**CRITICAL:** This guide documents YOUR PRODUCT/USER EXPERIENCE, not the context management framework.

Edit `docs/USER_GUIDE.md` to reflect:

- Your actual product/service (e.g., "How to use the webshop", not "How to use the framework")
- Your project-specific user workflows
- Your actual features and functionality
- Your domain-specific examples

Replace:

- `[YOUR PROJECT NAME]` with your actual project name
- All example webshop content with YOUR actual product details
- Agent workflow sections with YOUR USER workflows
- Remove template warnings once customized

**Example:** If building a webshop, USER_GUIDE.md should describe how customers shop and how admins manage products. It should NOT describe agent roles or brief creation workflows.

---

## Step 4: Configure System Prompts

Copy the system prompts from `docs/prompts/` to your AI assistant's configuration:

**For Cursor:**

- Open Cursor settings
- Find "Custom Instructions" or "System Prompts"
- Copy each prompt from `docs/prompts/system-*.txt`
- Configure for each agent role

**For Claude Code:**

- Use the prompts when initializing agents
- Reference them in agent configuration files

**For ChatGPT/Other:**

- Use the prompts as custom instructions
- Or paste into system message when starting conversations

---

## Step 5: Set Up Agent Specs

Review and customize agent specifications in `docs/agents/`:

1. **THINKING_BUDDY.md** - Review and adjust if needed for your workflow
2. **CODING_BUDDY.md** - Customize commit/versioning expectations if needed
3. **SYSTEM_BUDDY.md** - Review analysis scope for your system
4. **CONTEXT_STEWARD.md** - Customize operational boundaries for your tools

Most specs are tool-agnostic and should work as-is. Only customize if you have specific requirements.

---

## Step 6: Create Initial Documentation

### Update README.md

Add a reference to the context management framework in your project's main README.md:

```markdown
## Context Management

This project uses a structured context management framework. See:

- [User Guide](docs/USER_GUIDE.md) - How to use the system
- [System Summary](docs/system/SYSTEM_SUMMARY.md) - Technical documentation
- [Workflow Patterns](docs/WORKFLOW.md) - Agent collaboration patterns
```

### Create Initial SYSTEM_SUMMARY Entry

Add your first changelog entry to `docs/system/SYSTEM_SUMMARY.md`:

```markdown
### Version 1.0 - YYYY-MM-DD

**Status:** Initial Setup

**What Changed:**

- Initialized context management framework
- Set up documentation structure
- Configured agent roles and prompts

**Why:**

- Establish structured context management
- Enable predictable agent behavior
- Create sustainable documentation practices
```

---

## Step 7: Customize Templates (If Using Option A)

If you used Option A (Automated Customization) in Step 3, this step is already complete. If you used Option B (Manual), proceed to Step 8.

**If using Option A, verify customization:**

1. Check that `docs/USER_GUIDE.md` no longer contains `[YOUR PROJECT NAME]` placeholders
2. Check that `docs/system/SYSTEM_SUMMARY.md` no longer contains `[YOUR PROJECT NAME]` placeholders
3. Verify all example content has been replaced with your actual project details
4. Review both documents to ensure they accurately describe your project

If placeholders remain, ask THINKING_BUDDY to continue or manually complete the customization.

## Step 8: Test the Setup

### Test THINKING_BUDDY

1. Start a new conversation with your AI assistant
2. Use the THINKING_BUDDY start prompt from `docs/prompts/system-thinking-buddy.txt`
3. Provide a vague requirement (e.g., "I need a user authentication system")
4. Verify TB asks clarifying questions and creates a brief

### Test CODING_BUDDY

1. Create a brief manually or use one from THINKING_BUDDY
2. Start a new conversation
3. Use the CODING_BUDDY start prompt
4. Provide the brief
5. Verify CB implements from brief and doesn't expand scope

### Test SYSTEM_BUDDY

1. Start a new conversation
2. Use the SYSTEM_BUDDY start prompt
3. Request a system review
4. Verify SYSTEM creates findings document

---

## Step 8: Establish Documentation Maintenance

### Set Up Validation

Create a process to validate documentation freshness:

**Option A: Manual Review**

- Weekly review of documentation versions/dates
- Compare documentation to actual behavior

**Option B: Automated Checks**

- Create script to check version/date on all docs
- Run as part of CI/CD or weekly review

### Set Up Changelog Discipline

Ensure all system changes include changelog entries:

- Add to `docs/system/SYSTEM_SUMMARY.md` after every change
- Include: version, date, what changed, why, impact

---

## Customization Notes

### Project-Specific Customization

You may want to customize:

1. **Documentation Structure:**

   - Add project-specific sections to USER_GUIDE.md
   - Add domain-specific examples
   - Customize SYSTEM_SUMMARY.md structure

2. **Agent Behaviors:**

   - Adjust commit message formats in CODING_BUDDY.md
   - Customize versioning rules if needed
   - Add project-specific constraints

3. **Workflow Patterns:**
   - Add domain-specific workflows to WORKFLOW.md
   - Customize handoff artifacts if needed
   - Add project-specific escalation patterns

### Tool Integration

The framework is tool-agnostic, but you'll need to:

1. **Integrate with your CLI:**

   - Map concepts to your commands
   - Update USER_GUIDE.md with your command patterns

2. **Integrate with your project structure:**

   - Adjust file paths if needed
   - Update brief template for your project structure

3. **Integrate with your tools:**
   - Map external tools (issue trackers, etc.) to patterns
   - Update agent specs with tool-specific boundaries

---

## Verification Checklist

- [ ] **Read and understood `docs/RULES.md`** (CRITICAL - no manual code editing)
- [ ] Committed to letting agents write code (mindset shift complete)
- [ ] All files copied to project
- [ ] Work directories verified (already created: `work/briefs/`, `work/findings/`)
- [ ] **Project context folder populated** (`docs/project-context/` with your domain knowledge)
- [ ] **Created your own project-context files** - `docs/project-context/domain-requirements-EXAMPLE.md` is a template only - create your own `domain-requirements.md` (or similar) with actual project data
- [ ] Templates customized (Option A: via THINKING_BUDDY, Option B: manually)
- [ ] `[YOUR PROJECT NAME]` placeholders replaced in USER_GUIDE.md
- [ ] `[YOUR PROJECT NAME]` placeholders replaced in SYSTEM_SUMMARY.md
- [ ] Example content replaced with actual project details
- [ ] Template warnings removed or acknowledged
- [ ] SYSTEM_SUMMARY.md initialized in `docs/system/`
- [ ] System prompts configured in AI assistant
- [ ] Agent specs reviewed (customized if needed)
- [ ] Quality standards reviewed (`docs/QUALITY_STANDARDS.md`)
- [ ] Initial documentation created
- [ ] Tested with at least one agent
- [ ] Documentation maintenance process established
- [ ] Process for handling context drift understood

---

## Best Practices Setup

### Separate Agent Instances (Recommended)

**For best results, set up 4 separate agent conversations:**

1. Create a conversation with THINKING_BUDDY (use `docs/prompts/system-thinking-buddy.txt`)
2. Create a conversation with CODING_BUDDY (use `docs/prompts/system-coding-buddy.txt`)
3. Create a conversation with SYSTEM_BUDDY (use `docs/prompts/system-system-buddy.txt`)
4. Create a conversation with CONTEXT_STEWARD (use `docs/prompts/system-context-steward.txt`)

**Benefits:**

- Each agent maintains role fidelity
- Context stays focused per agent
- Clean handoffs between agents
- Easier to refresh context if drift occurs

**If using a single conversation:**

- Explicitly invoke agent roles when switching
- Use start prompts to re-establish boundaries
- Be clear about role transitions

### Context Refresh Strategy

**Plan for regular context refresh:**

- Re-invoke start prompts at the beginning of each work session
- Refresh when you notice agent drift (role boundary violations)
- Refresh before starting new work cycles (brief → implementation → review)

See `README.md` Best Practices section for detailed guidance on detecting and handling agent drift.

---

## Next Steps

1. **If you used Option A (Automated):** Review the customization brief created by THINKING_BUDDY and ensure all information is accurate
2. **If you used Option B (Manual):** Verify all placeholders are replaced and content is accurate
3. **Set up separate agent instances** (see Best Practices Setup above)
4. **Create your first brief** (see "Your First Brief" section below)
5. Use CODING_BUDDY to implement from brief
6. Run periodic SYSTEM_BUDDY reviews
7. Refine framework based on your experience

---

## Your First Brief

**After setup, create a simple first brief to understand the workflow.**

### Suggested First Brief Ideas

Choose a small, well-defined task that:

- Is clearly scoped (not ambiguous)
- Has obvious acceptance criteria
- Won't break anything if done wrong
- Is useful for your project

**Example first briefs:**

1. **Documentation update:**

   - "Add a 'Getting Started' section to README.md"
   - "Document the main entry point in README.md"
   - "Add installation instructions to README.md"

2. **Simple feature:**

   - "Add error handling to [specific function]"
   - "Add input validation to [specific form]"
   - "Add logging to [specific module]"

3. **Code quality:**
   - "Fix linting errors in [specific file]"
   - "Add type hints to [specific module]"
   - "Refactor [specific function] for clarity"

### First Brief Workflow

1. **Start with THINKING_BUDDY:**

   - Say: "I want to [describe your simple task]"
   - THINKING_BUDDY will ask clarifying questions
   - Answer questions until brief is complete

2. **Review the brief:**

   - THINKING*BUDDY creates brief at `work/briefs/YYYY-MM-DD*[name]\_brief.md`
   - Review it: Does it make sense? Are acceptance criteria clear?
   - Approve or request changes

3. **Hand to CODING_BUDDY:**

   - Say: "Please implement the brief at `work/briefs/YYYY-MM-DD_[name]_brief.md`"
   - CODING_BUDDY reads brief and implements
   - CODING_BUDDY adds Implementation Notes and archives brief

4. **Review the result:**
   - Check that implementation matches brief
   - Verify acceptance criteria are met
   - Review Implementation Notes to understand what was done

**This first brief helps you:**

- Understand the TB → brief → CB workflow
- See how briefs are structured
- Experience the review and approval process
- Learn how CB implements from briefs

**After your first brief:**

- You'll understand the workflow
- You can create more complex briefs
- You'll see the value of the separation (TB clarifies, CB implements)

See `README.md` for quick reference and `docs/USER_GUIDE.md` for detailed usage (once customized for your project).
