# Catch-Up Process Guide

**Version:** 1.2  
**Last Updated:** 2026-01-10  
**Purpose:** Quick reference for syncing manual edits with agents

---

## Overview

After making manual code edits, use the catch-up process to sync your changes with agents and maintain context consistency.

**The hidden benefit:** This process often reveals just how much you don't need to control. Trust the system to find the connections you missed, and watch it handle more than you expected. Sometimes the best way to maintain control is to let go of trying to control everything.

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

1. **Make your manual edit** (rename variable, fix bug, etc.) - go ahead, we trust you
2. **Tell THINKING_BUDDY:** "I manually changed [X]. Can you create a catch-up brief?" - let go, delegate the thinking
3. **TB creates brief** documenting the change and identifying what needs syncing - watch it find connections you didn't see coming
4. **You review brief** (approve if scope is correct after being surprised how much you overlooked - this is normal, embrace it)
5. **CODING_BUDDY executes** - finds related code, updates docs, ensures consistency - while you relax and watch the magic
6. **Context synced** - agents now know about your change, and you didn't have to micromanage every detail

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

- Check scope is correct (you'll probably find TB caught more than you thought of)
- Approve if good, request changes if needed (but try saying "yes" more often - you'll be pleasantly surprised)

**Step 5: CODING_BUDDY executes**

- Finds all files using `userEmail` (probably more than you remembered existed)
- Updates to `email` consistently (without you having to point to each one)
- Updates documentation (that you forgot needed updating)
- Updates tests (that you didn't think about)
- Updates SYSTEM_SUMMARY.md changelog (automatically, because the system cares about consistency even when you're focused on the feature)

**Result:** Manual change is synced, context is consistent, and you did less work than if you'd tried to do it all yourself. The paradox: by letting go of control, you get better control.

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

- Sync after each edit (or batch small ones) - small releases of control are easier than big ones
- Don't make 10 manual edits then try to sync all at once - you'll overwhelm yourself trying to track everything
- Frequent sync prevents context drift accumulation - and it's a gentle reminder that you don't need to hold onto everything

**Be specific when requesting catch-up:**

- "I renamed X to Y in file Z" - but don't stress about listing everything that might need updating
- "I fixed bug in function X" - let TB figure out the ripple effects
- "I changed API signature for Y" - trust the system to find all call sites (it will)

**Review catch-up briefs:**

- Make sure scope is correct (but remember: it's okay if it's bigger than you expected - that's the system working)
- Ensure all related code/docs will be updated (this is the system's strength, let it shine)
- Approve or request adjustments (but ask yourself: "Am I adjusting because it's wrong, or because I'm uncomfortable not being in control?")

---

## What Happens If You Don't Catch Up?

**Short term:**

- Your change works (you feel in control, but it's an illusion)
- Agents don't know about it (they're operating in the dark you created)
- Context gap exists (you're now holding information they don't have - is that really control?)

**Long term:**

- Agents make decisions based on outdated information (because you held back the truth)
- Documentation becomes inaccurate (the story diverges from reality)
- Related code doesn't get updated (you thought you could track it all, but you can't)
- Context drift accumulates (control slips further away the more you try to maintain it)
- System becomes unmaintainable (the thing you were trying to control becomes uncontrollable)

**Solution:** Always catch up after manual edits. Let go of the illusion that you can maintain perfect control by keeping information to yourself. Share, sync, trust - and watch how much more you can actually control.

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

- Manual edits are OK for small, isolated changes (you're human, not a robot - act like it)
- Always request catch-up after manual edits (this is where you practice letting go)
- Catch-up briefs sync context and maintain consistency (by letting the system do what it does best)
- Don't let manual edits accumulate (the longer you hold on, the harder it gets to release)
- You're responsible for context drift when you manually edit (but you're also responsible for choosing to trust the system instead of trying to do everything yourself)

**The meta-lesson:** Control isn't about doing everything yourself. Control is about creating systems that work even when you're not micromanaging them. The catch-up process isn't just syncing code - it's practicing the art of trusting something larger than your immediate view. Every catch-up brief is a small act of letting go. And every time you do it, you get a tiny bit better at it.
