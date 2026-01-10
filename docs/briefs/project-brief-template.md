# Project Brief: [Project Name]

**Version:** 1.0  
**Last Updated:** 2026-01-10  
**Purpose:** Template for creating project execution briefs

---

**Date:** YYYY-MM-DD  
**Created By:** THINKING_BUDDY  
**Status:** [Draft | Ready for Review | Approved | In Progress | Complete]

> **About Briefs:** This brief serves three functions: (1) **Role separation** - TB owns requirements, CB owns implementation; (2) **User review** - Your opportunity to approve or request changes before execution; (3) **Documentation** - Permanent record of what was requested and built. Review this brief before CB implements.

---

## Context and Goal

[One to two paragraphs describing the context, what problem is being solved, and why it matters. Include relevant background information.]

---

## Explicit Requirements

[Bulleted list of specific, unambiguous requirements. No implicit assumptions. Each requirement should be independently verifiable.]

- Requirement 1: [Specific, measurable requirement]
- Requirement 2: [Specific, measurable requirement]
- Requirement 3: [Specific, measurable requirement]

---

## Non-Goals

[Explicitly state what is NOT in scope. This prevents scope creep.]

- NOT doing: [What is explicitly out of scope]
- NOT doing: [Another out-of-scope item]
- NOT optimizing: [What optimization is deferred]

---

## Constraints and Rules

[Technical constraints, business rules, architectural constraints, or process rules that must be followed.]

- Constraint 1: [Specific constraint and why it exists]
- Constraint 2: [Another constraint]
- Rule: [Process or architectural rule]

---

## Acceptance Criteria

[Measurable, testable criteria that define "done". Each criterion should be independently verifiable.]

**IMPORTANT:** All acceptance criteria MUST be testable. CB will verify each criterion before closing.

- [ ] Criterion 1: [Specific, measurable outcome] - Verification method: [How to verify]
- [ ] Criterion 2: [Another measurable outcome] - Verification method: [How to verify]
- [ ] Criterion 3: [Verifiable result] - Verification method: [How to verify]

**Quality Gates (CB will validate all before closure):**
- [ ] All acceptance criteria met and verified
- [ ] Code quality standards satisfied
- [ ] Tests pass and coverage adequate
- [ ] Brief compliance verified
- [ ] Documentation updated (if required)
- [ ] Version/commit quality verified

---

## Standards or Processes to Follow

[Which standards, conventions, or processes should be followed during implementation.]

- Follow: [Standard or convention, e.g., "project code style guide"]
- Process: [Specific process, e.g., "TDD for all new features"]
- Convention: [Naming, structure, or other convention]

---

## Testing Expectations

[What testing is required. Be specific about scope and approach. CB must verify all tests pass before closure.]

- Unit tests: [What needs unit test coverage] - Expected coverage: [specific level if applicable]
- Integration tests: [What integration testing is needed]
- Manual testing: [What manual verification is required] - Steps: [specific steps to verify]
- Performance testing: [Any performance requirements] - Benchmarks: [specific metrics if applicable]
- Test validation: [ ] All tests must pass before closure

[If testing is not applicable or not required, state explicitly: "Testing: Not required for this brief" and explain why]

**Quality Standard:** All tests must pass. No test failures are acceptable. If tests fail, CB must fix before closing.

---

## Documentation Requirements

[What documentation must be updated as part of this implementation. Be explicit about what files need updating.]

- Update: [Documentation file and what section]
- Create: [New documentation if needed]
- Update: [Another documentation file]

[If documentation is not required, state explicitly: "Documentation: Not required for this brief"]

---

## Commit Discipline Expectations

[How commits should be structured. Use Conventional Commits format if applicable.]

- Format: [Commit message format, e.g., "Conventional Commits: `type(scope): subject`"]
- Granularity: [One commit or multiple commits?]
- Message requirements: [What must be included in commit messages]

---

## Version/Semantic Versioning Expectations

[Whether version bumping is required and what type (major/minor/patch).]

- Version bump: [Yes/No]
- Type: [Major | Minor | Patch | N/A]
- Reason: [Why this version bump type]
- **Version file location:** [Specify exact file path, e.g., "package.json", "Cargo.toml", "version.txt", "pyproject.toml"]
- **Version format:** [How version is stored, e.g., "Semantic version in 'version' field", "VERSION constant in version.rb"]

[If versioning is not applicable, state explicitly: "Versioning: Not applicable" and explain why]

**IMPORTANT:** CODING_BUDDY must know which file contains the version. If this is not specified, CB will escalate to TB.

---

## Handoff Note for CODING_BUDDY

[Brief note from THINKING_BUDDY to CODING_BUDDY. Should summarize key points and any special considerations.]

CB: [Direct note about implementation approach, potential gotchas, or important considerations. Keep this concise but helpful.]

---

## Implementation Notes

[This section is added by CODING_BUDDY after implementation. Leave blank until then.]

**Executed:** [YYYY-MM-DD HH:MM:SS]  
**Implemented By:** CODING_BUDDY

### What Was Implemented
[Summary of what was actually implemented]

### Deviations and Why
[Any deviations from the brief and why they were necessary. If no deviations, state: "No deviations from brief."]

### Files Changed
- [List of files that were modified or created]

### Follow-up Risks or Suggestions
[Any risks introduced, follow-up work needed, or suggestions for future improvements. If none, state: "No follow-up risks or suggestions."]

---

## Notes

[Any additional context, special considerations, or open questions. This section is optional and can be left blank if not needed.]

