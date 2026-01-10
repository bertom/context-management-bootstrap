# Catch-Up Process Guide

**Version:** 1.1  
**Last Updated:** 2026-01-10  
**Purpose:** Quick reference for syncing manual edits with agents

---

## Overview

After making manual code edits, use the catch-up process to sync your changes with agents and maintain context consistency.

---

## ⚠️ BEFORE Manual Edits: Check Context First

**If you see code that looks wrong or you don't understand, consult CONTEXT_STEWARD first.**

**Common scenario:** You see a function, variable, method, or pattern that looks wrong, and you're tempted to fix it manually.

**Why this matters:** What looks wrong to you might be intentional, part of a larger pattern, or have context you don't see. Editing without understanding can:
- Break things that work correctly
- Create unnecessary context drift
- Miss the actual problem

**Process:**
1. **Ask CONTEXT_STEWARD:** "This [function/variable/method] looks wrong. Can you check context and explain why it's implemented this way?"
2. **Understand first:** CONTEXT_STEWARD explains the context and whether it's actually wrong
3. **Then decide:** After understanding, decide if manual edit is appropriate or if a brief is needed

**See `docs/RULES.md` for detailed guidance on checking context before manual edits.**

## When to Use Catch-Up

**Use catch-up briefs after:**
- Variable/function renaming (after checking context if it looked wrong)
- Small refactors (after checking context if the original pattern looked wrong)
- Typo fixes that affect behavior
- Quick experiments you want to keep
- Any manual edit that affects code agents work with

**Don't need catch-up for:**
- Personal notes files
- External documentation (outside project)
- Files agents don't use

---

## Quick Process

1. **Make your manual edit** (rename variable, fix bug, etc.)
2. **Tell THINKING_BUDDY:** "I manually changed [X]. Can you create a catch-up brief?"
3. **TB creates brief** documenting the change and identifying what needs syncing
4. **You review brief** (approve if scope is correct)
5. **CODING_BUDDY executes** - finds related code, updates docs, ensures consistency
6. **Context synced** - agents now know about your change

---

## Example: Variable Rename

**Scenario:** You renamed `userEmail` to `email` in `auth.js`

**Step 1: Make the change manually**
```javascript
// auth.js - You manually changed this
const email = getUserEmail(); // was: const userEmail = getUserEmail();
```

**Step 2: Request catch-up**
```
You: "I manually renamed `userEmail` to `email` in auth.js. 
      Can you create a catch-up brief to sync this change?"
```

**Step 3: THINKING_BUDDY creates brief**
- Brief documents: `userEmail` → `email` in auth.js
- Brief identifies: Find all references to `userEmail`, update to `email`
- Brief scope: Update related code, docs, tests

**Step 4: You review brief**
- Check scope is correct
- Approve if good, request changes if needed

**Step 5: CODING_BUDDY executes**
- Finds all files using `userEmail`
- Updates to `email` consistently
- Updates documentation
- Updates tests
- Updates SYSTEM_SUMMARY.md changelog

**Result:** Manual change is synced, context is consistent

---

## Example: Quick Fix

**Scenario:** You fixed a typo in a function name (`proccessData` → `processData`)

**Process:**
1. Fix typo manually
2. Request catch-up: "I fixed typo `proccessData` → `processData` in utils.js"
3. TB creates brief to find all references and update
4. CB updates all references, docs, tests
5. Context synced

---

## Risk Assessment

**Low risk (still need catch-up):**
- Variable/function renaming
- Typo fixes
- Small refactors
- Formatting changes

**Medium risk (definitely need catch-up):**
- Adding functions
- Changing API signatures
- Modifying data structures

**High risk (create brief immediately):**
- Architecture changes
- Core logic changes
- Behavior changes

**Rule of thumb:** If it affects code agents work with, request catch-up.

---

## Tips

**Don't accumulate manual edits:**
- Sync after each edit (or batch small ones)
- Don't make 10 manual edits then try to sync all at once
- Frequent sync prevents context drift accumulation

**Be specific when requesting catch-up:**
- "I renamed X to Y in file Z"
- "I fixed bug in function X"
- "I changed API signature for Y"

**Review catch-up briefs:**
- Make sure scope is correct
- Ensure all related code/docs will be updated
- Approve or request adjustments

---

## What Happens If You Don't Catch Up?

**Short term:**
- Your change works
- Agents don't know about it
- Context gap exists

**Long term:**
- Agents make decisions based on outdated information
- Documentation becomes inaccurate
- Related code doesn't get updated
- Context drift accumulates
- System becomes unmaintainable

**Solution:** Always catch up after manual edits.

---

## Quick Reference

**After manual edit:**
```
"I manually changed [what] in [file]. Can you create a catch-up brief?"
```

**TB will:**
- Create brief documenting the change
- Identify what needs syncing (related code, docs, tests)
- Brief ready for your review

**After approving brief:**
- CB executes catch-up
- Finds and updates all related references
- Updates documentation
- Updates SYSTEM_SUMMARY.md
- Context is now consistent

---

## Remember

- Manual edits are OK for small, isolated changes
- Always request catch-up after manual edits
- Catch-up briefs sync context and maintain consistency
- Don't let manual edits accumulate
- You're responsible for context drift when you manually edit

