# Troubleshooting Guide

**Version:** 1.0  
**Last Updated:** 2026-01-10  
**Purpose:** Common issues and solutions for the context management framework

---

## Overview

This guide addresses common problems you may encounter when using the context management framework and provides solutions.

---

## Agent Drift Issues

### Problem: Agent Acting Outside Role Boundaries

**Symptoms:**
- CODING_BUDDY creating briefs or clarifying requirements
- THINKING_BUDDY writing code or implementing features
- SYSTEM_BUDDY creating briefs or implementing fixes
- CONTEXT_STEWARD writing code or creating briefs

**Solution:**
1. **Immediate refresh:**
   - Re-invoke the agent's start prompt (`docs/prompts/system-[agent-name].txt`)
   - Agent should acknowledge with "READY" and reset to proper role

2. **Reference agent specification:**
   - Point agent to `docs/agents/[AGENT_NAME].md`
   - Remind agent of its specific role and what it should NOT do

3. **If drift persists:**
   - Start a fresh conversation with the agent
   - Use start prompt to initialize cleanly
   - Copy relevant context (briefs, findings) as needed

4. **Prevention:**
   - Refresh context regularly (daily or per task)
   - Keep separate agent instances (one conversation per agent)
   - Monitor for early signs of drift

**Prevention:** Refresh agent context at start of each work session. See `README.md` Best Practices section.

---

### Problem: Agent Consistently Drifts Despite Refresh

**Symptoms:**
- Agent keeps drifting even after refresh
- Agent "forgets" role boundaries quickly
- Multiple refreshes needed per session

**Solution:**
1. **Check conversation length:**
   - If >100 messages, start fresh conversation
   - Long conversations increase drift risk

2. **Verify start prompt:**
   - Ensure you're using correct start prompt
   - Check that prompt hasn't been modified incorrectly

3. **Check agent specification:**
   - Verify agent spec file hasn't been modified
   - Ensure spec clearly defines role boundaries

4. **Consider agent limitations:**
   - Some AI models may have difficulty maintaining role fidelity
   - May need more frequent refreshes or stricter boundaries

**Prevention:** Keep conversations focused. Start fresh conversations for new work cycles.

---

## Brief Quality Issues

### Problem: Briefs Keep Getting Rejected by User

**Symptoms:**
- User repeatedly requests changes to briefs
- Briefs don't capture requirements correctly
- THINKING_BUDDY not asking enough questions

**Solution:**
1. **For THINKING_BUDDY:**
   - Remind TB to ask more clarifying questions
   - Point TB to its specification: "You must ask clarifying questions until ambiguity is zero"
   - Request TB to restate requirements before creating brief

2. **For user:**
   - Provide more detail when describing requirements
   - Answer TB's questions fully
   - Review brief carefully before approving

3. **Improve brief template:**
   - Ensure brief includes all required sections
   - Add more specific acceptance criteria
   - Include examples or references

**Prevention:** THINKING_BUDDY should ask questions until zero ambiguity. Don't rush brief creation.

---

### Problem: CODING_BUDDY Keeps Escalating Due to Unclear Briefs

**Symptoms:**
- CB frequently escalates to TB for clarification
- Briefs are missing information
- CB can't proceed without asking questions

**Solution:**
1. **For THINKING_BUDDY:**
   - Review brief before exporting
   - Ensure all acceptance criteria are testable
   - Verify all required information is included
   - Ask: "Can CB implement this without asking questions?"

2. **For brief quality:**
   - Use brief template checklist
   - Ensure brief is complete and unambiguous
   - Include all technical details CB needs

3. **For CB escalations:**
   - CB is correct to escalate if brief is unclear
   - Don't ask CB to guess - fix the brief instead
   - TB should revise brief based on CB's feedback

**Prevention:** THINKING_BUDDY should validate brief completeness before export. Brief must be executable without questions.

---

### Problem: Brief Revision During Active Implementation

**Symptoms:**
- Brief needs major revision while CB is implementing
- Partial work exists from old brief
- Unclear whether to continue or start fresh

**Solution:**
1. **CB should:**
   - Stop current implementation
   - Document current state in Implementation Notes
   - Assess: Can partial work be salvaged or must rollback?

2. **TB should:**
   - Create revised brief with new name (e.g., add `_v2` suffix)
   - Include in revised brief: "Continue from [point] or start fresh?"
   - Specify what to keep vs. what to change

3. **User should:**
   - Review revised brief carefully
   - Decide: Continue from partial work or start fresh
   - Approve revised brief

4. **CB continues:**
   - Compare old vs. new brief
   - Follow revised brief instructions
   - Document what changed in Implementation Notes

**Prevention:** Review briefs carefully before approval. Changes after implementation starts are disruptive.

---

## Context Drift Issues

### Problem: Context Drift Accumulating Despite Catch-Up Process

**Symptoms:**
- Agents seem confused about codebase state
- Documentation doesn't match code
- Briefs reference code that was manually changed
- SYSTEM_BUDDY findings don't match understanding

**Solution:**
1. **Immediate recovery:**
   - Stop making manual edits
   - Request SYSTEM_BUDDY system review
   - SYSTEM will identify drift and create findings

2. **Restore alignment:**
   - TB creates briefs to align documentation with code
   - Or: TB creates briefs to align code with documentation
   - CB implements alignment fixes

3. **Re-establish discipline:**
   - Commit to using briefs for all changes
   - Request catch-up briefs immediately after manual edits
   - Don't let manual edits accumulate

4. **Prevention:**
   - Always request catch-up brief after manual edits
   - Sync frequently (don't batch manual edits)
   - Use briefs for anything affecting multiple files

**Prevention:** Always sync manual edits immediately. Don't accumulate manual changes.

---

### Problem: Manual Edits Not Being Caught Up

**Symptoms:**
- Manual edits made but catch-up brief not created
- Related code/docs not updated
- Context gaps remain

**Solution:**
1. **Create catch-up brief immediately:**
   - Tell THINKING_BUDDY: "I manually changed [X]. Can you create a catch-up brief?"
   - Describe what changed and where
   - TB creates brief to sync context

2. **Review catch-up brief:**
   - Ensure scope includes all related code/docs
   - Approve if correct, request changes if needed

3. **Execute catch-up:**
   - CB implements catch-up brief
   - Updates all related references
   - Updates documentation
   - Updates SYSTEM_SUMMARY.md

**Prevention:** Make catch-up briefs part of your workflow. Don't skip them.

---

## Quality Gate Issues

### Problem: Quality Gates Keep Failing

**Symptoms:**
- CB can't complete implementation due to failing quality gates
- Tests keep failing
- Linting errors persist
- Documentation updates incomplete

**Solution:**
1. **For CB:**
   - Fix quality issues before proceeding
   - Don't close implementation with failing gates
   - Escalate to TB if quality gates can't be satisfied due to brief issues

2. **For brief:**
   - Ensure brief specifies quality requirements
   - Include testing expectations
   - Specify documentation requirements

3. **For user:**
   - Review quality gate failures
   - Determine if brief needs revision
   - Consider if "good enough" is acceptable (document why)

4. **Escalation:**
   - If quality gates keep failing: Review brief for completeness
   - If brief is incomplete: TB should revise
   - If technical issues: CB should escalate to TB

**Prevention:** Brief should specify all quality requirements. CB should validate before starting.

---

### Problem: Quality Gates Too Strict

**Symptoms:**
- Quality gates block reasonable implementations
- Perfectionism preventing progress
- Gates failing for minor issues

**Solution:**
1. **Review quality standards:**
   - Are standards appropriate for project stage?
   - Can standards be relaxed for MVP/prototype?
   - Document exceptions in brief

2. **Brief should specify:**
   - Quality expectations (strict vs. pragmatic)
   - What quality gates are required
   - What can be deferred

3. **User decision:**
   - Review failing quality gates
   - Decide: Fix now or defer
   - Document decision in brief or Implementation Notes

**Prevention:** Brief should specify quality expectations. Match standards to project needs.

---

## Workflow Issues

### Problem: Agents Bypassing Workflow

**Symptoms:**
- SYSTEM_BUDDY creating briefs directly
- CONTEXT_STEWARD routing directly to CB
- Agents skipping TB in workflow

**Solution:**
1. **Remind agent of workflow:**
   - SYSTEM → findings → TB → brief → CB
   - Never skip TB in workflow
   - All implementation goes through briefs

2. **Refresh agent context:**
   - Re-invoke start prompt
   - Reference workflow documentation
   - Point to `docs/WORKFLOW.md`

3. **Enforce boundaries:**
   - Don't accept work that bypasses workflow
   - Redirect to proper workflow
   - Maintain discipline

**Prevention:** Regular context refresh. Clear workflow documentation.

---

### Problem: Brief Not Being Reviewed Before Implementation

**Symptoms:**
- CB starts implementation before user reviews brief
- Brief changes after CB starts
- User didn't approve brief

**Solution:**
1. **For CB:**
   - Check brief status before starting
   - If status is "Ready for Review": Wait for user approval
   - Only start if brief is "Approved" or explicitly approved by user

2. **For user:**
   - Review briefs before approving
   - Don't skip review step
   - Approve explicitly: "Brief approved, CB can proceed"

3. **For workflow:**
   - Brief status should be clear
   - TB should wait for approval before handoff
   - CB should verify approval before starting

**Prevention:** Always review briefs before approval. CB should verify approval.

---

## System Health Review Issues

### Problem: SYSTEM_BUDDY Not Suggesting Reviews

**Symptoms:**
- No proactive review suggestions
- Reviews not happening regularly
- Tracking file issues

**Solution:**
1. **Check tracking file:**
   - Verify `work/findings/last_review_date.txt` exists
   - Check file format: `YYYY-MM-DD [A|B]`
   - If missing: Create manually or let SYSTEM create on next review

2. **Manual review:**
   - Request SYSTEM_BUDDY review manually
   - Use prompt: `docs/prompts/system-health-review.txt`
   - Specify cadence (Option A or B)

3. **Check SYSTEM_BUDDY:**
   - Verify SYSTEM_BUDDY is checking tracking file
   - Refresh SYSTEM_BUDDY context if needed
   - Ensure proactive suggestion is enabled

**Prevention:** SYSTEM_BUDDY should check tracking file before interactions. Manual reviews are always available.

---

### Problem: Tracking File Format Issues

**Symptoms:**
- SYSTEM_BUDDY can't read tracking file
- Wrong format in tracking file
- File missing or corrupted

**Solution:**
1. **Fix file format:**
   - File: `work/findings/last_review_date.txt`
   - Format: Single line `YYYY-MM-DD [A|B]`
   - Example: `2026-01-10 A`

2. **Recreate file:**
   - Delete corrupted file
   - Let SYSTEM_BUDDY create new file on next review
   - Or create manually with correct format

3. **Fallback:**
   - SYSTEM_BUDDY should check findings files if tracking file missing
   - Extract date from most recent findings filename
   - Use that as last review date

**Prevention:** SYSTEM_BUDDY should validate file format when reading. Always document review date in findings file (backup).

---

## Getting Help

### When to Escalate

**Escalate to user if:**
- Workflow is completely broken
- Agents consistently fail despite refresh
- Quality gates blocking all progress
- Context drift too severe to recover

**Escalate to SYSTEM_BUDDY if:**
- System-wide issues detected
- Workflow patterns breaking
- Agent boundary violations frequent
- Documentation drift severe

**Escalate to CONTEXT_STEWARD if:**
- Tool usage questions
- Operational guidance needed
- Workflow clarification needed

---

## Prevention Checklist

**Daily:**
- [ ] Refresh agent contexts at start of session
- [ ] Review briefs before approving
- [ ] Sync manual edits immediately

**Weekly:**
- [ ] Run SYSTEM_BUDDY light review
- [ ] Check for context drift
- [ ] Review agent role fidelity

**Monthly:**
- [ ] Run SYSTEM_BUDDY deep review
- [ ] Review workflow effectiveness
- [ ] Update documentation as needed

---

## Still Having Issues?

If problems persist:
1. Review `docs/RULES.md` for context drift prevention
2. Review `docs/WORKFLOW.md` for workflow patterns
3. Review agent specifications in `docs/agents/`
4. Consider starting fresh with new agent conversations
5. Document the issue for SYSTEM_BUDDY to analyze

