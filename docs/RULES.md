# Rules for Using This Framework

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** Critical rules that must be followed for the framework to work

---

## ⚠️ Context Drift and Manual Editing

### The Reality

**You can manually edit code files, but you are responsible for context drift.**

Manual edits create a gap between what you know and what agents know. This gap is called "context drift" and it breaks the context management system if not addressed.

---

## Why This Rule Exists

### Context Drift

Agents reason from **context**:
- The actual codebase files
- Documentation (USER_GUIDE.md, SYSTEM_SUMMARY.md)
- Briefs and findings
- Implementation history
- Agent conversation context

When you manually edit files:
- Agents don't know about your changes
- Documentation becomes inaccurate
- Briefs become out of sync
- System understanding diverges from reality
- **Context drift occurs**

### The Context Gap

**You know:** What you just changed manually  
**Agents know:** What's in the files, documentation, and conversation history

**The gap:** Manual edits create a divergence between what you know and what agents know.

Agents make decisions based on:
- Codebase analysis
- Documentation state
- Brief specifications
- Previous implementation notes

If you change files manually, agents will:
- Make decisions based on outdated information
- Document incorrectly
- Create briefs that don't match reality
- Implement features that conflict with your manual changes

---

## Manual Editing: Understanding the Tradeoff

### The Default Workflow (Recommended)

**For most changes, use the brief → implementation workflow:**
1. Ask THINKING_BUDDY to create a brief
2. CODING_BUDDY implements from brief
3. Context stays consistent, documentation accurate

**Benefits:**
- Context consistency maintained
- Documentation automatically updated
- Agents can reason about full system
- Quality gates enforced

### When Manual Editing is Acceptable

**You may manually edit code for:**
- **Small, isolated fixes:** Variable renaming, typo fixes, simple refactors
- **Quick experiments:** Trying something out before creating a brief
- **Personal preference:** Code style adjustments that don't affect behavior

**You are responsible for:**
- Ensuring agents catch up with your changes
- Documenting changes that affect system behavior
- Maintaining context consistency yourself

### The Catch-Up Process (After Manual Edits)

**After making manual edits, you MUST sync with agents:**

1. **Notify THINKING_BUDDY about the change:**
   - Tell TB what you changed manually
   - Explain why (if relevant)
   - Request a catch-up brief

2. **THINKING_BUDDY creates catch-up brief:**
   - Brief documents your manual change
   - Brief identifies what else needs updating (related code, docs, tests, etc.)
   - Brief ensures consistency across the codebase

3. **CODING_BUDDY executes catch-up:**
   - Finds and updates all related references
   - Updates documentation
   - Updates tests if needed
   - Updates SYSTEM_SUMMARY.md changelog
   - Ensures consistency

**Example workflow:**

```
You: "I manually renamed `userEmail` to `email` in auth.js. Can you create a brief to sync this change?"

TB: Creates brief: "Catch-up: Document variable rename and update all references"
- What changed: `userEmail` → `email` in auth.js
- Scope: Find all instances of `userEmail`, update to `email`, update docs/tests
- Acceptance: All references updated, docs updated, tests pass

CB: Executes brief:
- Finds all files using `userEmail`
- Updates to `email` consistently
- Updates documentation mentioning the variable
- Updates tests
- Updates SYSTEM_SUMMARY.md changelog
```

**Result:** Manual change is synced, context is consistent, documentation is accurate.

**The brief serves to:**
- Document what you changed manually
- Ensure all related code/docs are updated
- Maintain context consistency
- Update SYSTEM_SUMMARY.md changelog

### Risk Assessment

**Low-risk manual edits (still need catch-up):**
- Variable/function renaming (agents can find all references)
- Typo fixes in comments
- Formatting/style changes
- Small refactors (extract function, move code)

**Medium-risk manual edits (definitely need catch-up):**
- Adding new functions/features
- Changing API signatures
- Modifying data structures
- Updating configuration

**High-risk manual edits (create brief immediately):**
- Changing core architecture
- Modifying critical business logic
- Updating external interfaces
- Changing behavior that affects users

**After any manual edit:**
- Assume agents don't know about it
- Request catch-up brief to sync context
- Don't let manual edits accumulate

---

## The Mindset Shift

### Accept These Truths

**You can write code, but agents maintain context.**

The framework is designed for **AI-assisted development with context management**. You are:
- The strategic decision maker
- The requirements clarifier (through THINKING_BUDDY)
- The quality reviewer (reviewing agent output)
- The blocker handler (credentials, approvals, missing info)
- **The code editor** (you can write/edit code, but must sync with agents)

**However:**
- Agents maintain system-wide context (documentation, related code, tests)
- Manual edits create gaps agents can't see
- You're responsible for syncing manual changes with agents
- Briefs ensure changes are properly documented and propagated

### When to Use Briefs vs. Manual Edits

**Use briefs for:**
- Features and significant changes
- Anything that affects multiple files
- Changes that need documentation
- Changes that need testing
- Anything that affects system behavior

**Manual edits are OK for:**
- Small, isolated fixes (rename variable, fix typo)
- Quick experiments
- Personal code style preferences

**But always:**
- Request catch-up brief after manual edits
- Don't let manual edits accumulate
- Be aware you're taking responsibility for context consistency

### Understanding the Tradeoff

**Manual edits are faster in the short term:**
- You fix it, it's done
- No brief creation, no agent round-trip
- Immediate gratification

**But manual edits create debt:**
- Agents don't know about the change
- Documentation may become inaccurate
- Related code may not be updated
- Context drift accumulates over time

**The catch-up process:**
- Brief documents your manual change
- Agents find and update related code/docs
- Context consistency restored
- Documentation stays accurate

**Balance:**
- Use manual edits when appropriate (small, isolated changes)
- Always request catch-up brief after manual edits
- Don't accumulate manual edits (sync frequently)
- Use briefs for anything that affects system behavior or multiple files

---

## What You CAN Edit Manually

### Safe to Edit Manually

These files are safe to edit manually (agents don't reason from them):
- Personal notes
- Meeting notes
- External documentation (outside the project)
- Configuration files for tools agents don't use
- `.gitignore` (usually safe, but check if agents use it)

### Template Customization Exception (One-Time Only)

**During initial setup only:** You may manually edit template files (`docs/USER_GUIDE.md`, `docs/system/SYSTEM_SUMMARY.md`) **ONCE** during initial project setup to replace placeholders.

**Why this exception exists:**
- Templates contain placeholders that must be replaced (`[YOUR PROJECT NAME]`, example content)
- This is a one-time initialization task
- After customization, these become project files and follow normal rules

**Rules for template customization:**
- **Only during initial setup** (Step 3 in SETUP.md)
- **Only for replacing placeholders** - Don't add new content or restructure
- **Preferred:** Use Option A (automated via THINKING_BUDDY setup prompt) instead
- **After customization:** These files become project files, normal rules apply

**Important:** This is a **one-time exception**. After templates are customized, they are subject to the normal no-manual-editing rule.

### Framework Customization Exception (One-Time Only)

**During initial setup only:** You may customize framework files (agent specs in `docs/agents/`, prompts in `docs/prompts/`) to match your project's needs.

**Why this exception exists:**
- Framework files may need project-specific customization
- Agent behaviors may need adjustment for your domain
- One-time customization during setup is acceptable

**Rules for framework customization:**
- **Only during initial setup** - Customize once, then treat as project files
- **After setup:** Changes to framework files should go through briefs (especially if they affect agent behavior)
- If customizing framework files creates context drift, restore alignment via briefs

**Important:** After setup, framework files follow normal rules. Changes that affect agent behavior should go through briefs.

### Check Before Editing

**If in doubt, ask CONTEXT_STEWARD:**
- "Is it safe to edit [file] manually?"
- "Should I create a brief for this change instead?"
- "Is this covered by a setup exception?"

### When Manual Edits Are Necessary (Emergency Exception)

**Emergency situations only:** When the system is in a state where agents cannot function and brief creation workflow is impossible:

- System is completely broken and agents can't fix it (tooling broken, context completely corrupted)
- Security issue that needs immediate fix (data breach, exposed credentials)
- Production incident requiring immediate hotfix (system down, data loss risk)

**Emergency procedure:**
1. **Fix the immediate issue manually** (break the rule - it's necessary in true emergencies)
2. **Immediately document** what you changed in a text file (timestamp, what changed, why)
3. **As soon as system is functional:** Create brief documenting the emergency fix
4. **Have CODING_BUDDY review and properly implement** the fix through normal workflow
5. **Replace manual fix:** If possible, revert manual changes and replace with agent-implemented version
6. **Update changelog:** Update `docs/system/SYSTEM_SUMMARY.md` changelog via brief

**Key principle:** Manual emergency fixes are **temporary**. Agent fixes through proper workflow are **permanent**. Brief documents both.

**This is not an excuse for convenience.** Only use in true emergencies where the workflow is impossible.

---

## Context Drift Detection and Recovery

### Signs of Context Drift

You may have context drift if:
- Agents suggest changes to code you already modified
- Documentation describes behavior that doesn't match code
- Briefs reference code that was manually changed
- Agents seem "confused" about the codebase state
- SYSTEM_BUDDY findings don't match your understanding

### Recovery Process

If you suspect context drift:

1. **Stop making manual changes**
2. **Let SYSTEM_BUDDY review:**
   - Request a system review
   - SYSTEM will identify drift
   - SYSTEM creates findings

3. **Restore alignment:**
   - THINKING_BUDDY creates briefs to align documentation
   - CODING_BUDDY updates files to match documentation
   - Or: Update documentation to match reality (via brief)

4. **Re-establish discipline:**
   - Commit to using briefs for all changes
   - Ask CONTEXT_STEWARD before any manual edits
   - Review these rules

---

## Your Responsibility

### Awareness, Not Prohibition

**You are responsible for context drift when you manually edit.**

Agents cannot prevent you from manually editing files. This is **your responsibility to manage**.

**Before editing any file manually, assess:**
- "Is this a small, isolated change or something larger?"
- "Will this affect multiple files or system behavior?"
- "Can I sync this change with agents afterward?"

**After manual edits:**
- Request catch-up brief to sync context
- Don't let manual edits accumulate
- Be aware you're taking responsibility for maintaining context consistency

### Accountability

**Track your manual edits:**
- Note what you changed manually
- Request catch-up briefs promptly
- Don't accumulate manual edits (sync frequently)

**Review your patterns:**
- Weekly: How many manual edits did you make? Did you sync them?
- Monthly: Is context drift accumulating? Are agents confused?
- Quarterly: Is documentation still accurate? Are agents working from correct context?

---

## Benefits of Following This Rule

### Context Consistency

- Agents always have accurate context
- Documentation matches codebase
- Briefs are based on current reality
- System understanding stays aligned

### Better Quality

- Agents can reason about the full system
- Changes are documented automatically
- Changelog stays accurate
- Quality gates work correctly

### Long-Term Sustainability

- System remains maintainable
- Onboarding new agents is easier
- Context is preserved over time
- Documentation stays useful

### Reduced Cognitive Load

- You don't need to remember what you changed
- Agents track everything
- Documentation is always current
- System is self-documenting

---

## Common Excuses (And Why They're Wrong)

### "It's just a small fix"

**Reality:** Small fixes are OK, but they still need sync.

Every manual edit creates a context gap. Multiple small edits create multiple gaps. But you can fix small things manually - just sync afterward.

**Better approach:** 
- Small fixes: Manual edit is fine, but request catch-up brief
- Multiple small fixes: Consider batching into one brief
- Sync frequently to prevent gap accumulation

### "I can fix it faster manually"

**Reality:** Manual speed is real, but creates debt.

You save time manually, but must sync afterward. The catch-up brief takes time. Balance speed vs. context debt.

**Better approach:** 
- Quick fixes: Manual edit, then catch-up brief
- Significant changes: Use brief workflow from the start
- Balance: Speed when appropriate, sync to maintain context

### "The code is obviously wrong"

**Reality:** Obvious fixes can be manual, but sync afterward.

If it's obvious, fix it manually. But then request a catch-up brief so agents can update related code/docs and maintain context.

**Better approach:** Fix it manually if you want, then: "TB, I fixed [obvious issue]. Can you create a brief to document this and update related code/docs?"

### "Agents made a mistake, I need to fix it"

**Reality:** You can fix it manually, but sync afterward.

If agents made a mistake, fix it manually if you want. But then create a catch-up brief so the fix is properly documented and agents learn from it.

**Better approach:** Fix manually, then: "TB, I fixed [mistake]. Can you create a brief documenting this fix and ensuring related code/docs are updated?"

---

## Summary

**The Reality:** You can manually edit code, but you are responsible for context drift.

**The Risk:** Manual edits create gaps between what you know and what agents know. This breaks context management if not addressed.

**The Process:** After manual edits, request a catch-up brief to sync context. Briefs document changes, update related code/docs, and maintain consistency.

**The Balance:** 
- Manual edits OK for small, isolated changes
- Use briefs for features and significant changes
- Always sync manual edits with agents via catch-up briefs
- Don't let manual edits accumulate

**The Mindset:** You can code. Agents maintain context. Sync your changes with agents to keep context consistent.

**The Benefit:** Flexibility to work quickly when needed, with processes to maintain long-term context consistency and documentation accuracy.

---

## Next Steps

1. **Commit to this rule** - Accept that manual coding is not part of this workflow
2. **Set up safeguards** - Ask CONTEXT_STEWARD before manual edits
3. **Trust the process** - Even when agents make mistakes, let them fix it
4. **Review regularly** - Check for context drift, restore discipline if needed

**Remember:** Context drift is the enemy. Briefs are the solution. Agents are the implementers. You are the strategist.

