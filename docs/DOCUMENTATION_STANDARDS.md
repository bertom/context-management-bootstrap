# Documentation Standards and Maintenance Guidelines

**Version:** 1.2  
**Last Updated:** 2026-01-10  
**Purpose:** Comprehensive standards and guidelines for documentation creation, maintenance, and quality

---

## Overview

This document defines the standards, maintenance responsibilities, and processes for all documentation in the context management framework. **All agents MUST follow these standards when creating or updating documentation.**

Documentation is a critical component of context management. Accurate, current, and well-maintained documentation ensures:
- Context consistency between agents and users
- Reduced context drift
- Clear understanding of system state and behavior
- Effective collaboration and handoffs
- Long-term maintainability

---

## Core Principles

1. **Documentation as Truth:** Documentation must accurately reflect reality, not aspirations
2. **Version Tracking:** All documentation must have version numbers and update dates
3. **Ownership:** Each document type has clear ownership and maintenance responsibilities
4. **Proactive Maintenance:** Documentation is updated as part of implementation, not as an afterthought
5. **Consistency:** Format, style, and structure are consistent across all documentation
6. **Accessibility:** Documentation is organized, findable, and readable

---

## Document Header Standards (MANDATORY)

**Every documentation file MUST include a header with:**

```markdown
# Document Title

**Version:** X.Y [or X.Y.Z]  
**Last Updated:** YYYY-MM-DD  
**Purpose:** Brief description of the document's purpose

---
```

### Version Numbering

**Format:** `X.Y` or `X.Y.Z`

- **Major version (X.0 → X+1.0):** Significant structural changes, new major sections, breaking changes to format or approach
- **Minor version (X.Y → X.Y+1):** New sections, major additions to existing sections, significant content expansions
- **Patch version (X.Y → X.Y.Z):** Corrections, clarifications, minor additions, typo fixes, formatting improvements

**Examples:**
- `1.0 → 2.0` - Complete restructure or major new sections
- `1.0 → 1.1` - Added new section or significant expansion
- `1.0 → 1.0.1` - Fixed typo, clarified wording, minor formatting

### Date Format

**Format:** `YYYY-MM-DD` (ISO 8601)

**Update Requirement:** Date MUST be updated to today's date whenever ANY content in the document is modified, including:
- Content changes
- Formatting corrections
- Structural changes
- Version updates

### Update Process (CRITICAL)

**When updating ANY documentation file:**

1. **Update header FIRST** - Update version number and date BEFORE or DURING the edit, not after
2. **Update content** - Make the actual changes
3. **Verify header** - Ensure version and date are correct before finalizing

**Why this matters:** Outdated version/date information misleads readers about document currency and violates trust in the documentation system.

---

## Documentation Structure and Organization

### Documentation Categories

**1. Framework Documentation** (`docs/`)
- `README.md` - Framework overview and quick start
- `RULES.md` - Critical rules and context drift management
- `WORKFLOW.md` - Workflow patterns and collaboration protocols
- `QUALITY_STANDARDS.md` - Quality standards and validation criteria
- `DOCUMENTATION_STANDARDS.md` - This document
- `CATCHUP_GUIDE.md` - Quick reference for catch-up process
- `TROUBLESHOOTING.md` - Common issues and solutions

**2. System Documentation** (`docs/system/`)
- `SYSTEM_SUMMARY.md` - System summary, actual behavior, and changelog
- Living documentation that reflects current system state

**3. Project Documentation** (`docs/`)
- `USER_GUIDE.md` - User-facing guide template (customized per project)
- `DECISIONS.md` - Decision log template (customized per project)

**4. Agent Specifications** (`docs/agents/`)
- `THINKING_BUDDY.md`
- `CODING_BUDDY.md`
- `SYSTEM_BUDDY.md`
- `CONTEXT_STEWARD.md`

**5. Prompts** (`docs/prompts/`)
- System prompts (`system-*.txt`)
- Setup prompts (`setup-*.txt`)
- Review prompts (`*-review.txt`)

**6. Templates** (`docs/briefs/`)
- `project-brief-template.md`
- `quality-checklist-template.md`

**7. Project Context** (`docs/project-context/`)
- READ-ONLY project-specific domain knowledge
- Business rules, requirements, API specifications
- **DO NOT MODIFY** unless explicitly requested by user

### File Naming Conventions

- **Markdown files:** Use `UPPERCASE.md` for main documentation files, `lowercase.md` for supporting files
- **Prompt files:** Use `lowercase-with-hyphens.txt`
- **Example files:** Use `*-EXAMPLE.md` suffix (agents must ignore these)
- **Consistent naming:** Follow existing patterns in the repository

---

## Agent Documentation Responsibilities

### CODING_BUDDY (Primary Documentation Maintainer)

**Owns:** Code and documentation maintenance

**Responsible for updating:**

1. **`docs/system/SYSTEM_SUMMARY.md`** (MANDATORY after implementation)
   - Add changelog entry with:
     - Version number
     - Date (YYYY-MM-DD)
     - Status: Enhancement/Fix/Redesign/Breaking
     - What changed (brief summary - concise, high-level)
     - Brief reference (link to archived brief for detailed implementation context)
     - System-level decisions (if brief contains "System-Level Decisions" section - extract decisions, trade-offs, rationale)
     - Impact (what this affects)
     - Files modified
   - **Extraction from brief:**
     - If brief has "System-Level Decisions" section: Extract to SYSTEM_SUMMARY changelog entry
     - If brief does NOT have system-level decisions: Omit or state "No system-level decisions - standard implementation"
     - Always include brief reference for detailed implementation context
   - Update relevant sections if system behavior changed
   - Update version and date in header

2. **`docs/USER_GUIDE.md`** (when system behavior changes)
   - Update relevant sections to reflect new behavior
   - Update workflows if processes changed
   - Maintain consistency in formatting and style
   - Update version and date in header

3. **Root `README.md`** (when framework structure or setup changes)
   - Update structure diagram if needed
   - Update setup instructions if changed
   - Update version and date if modified

4. **Code-level documentation** (when brief requires)
   - Code comments
   - Function/method documentation
   - Package/component README files
   - API documentation

**Update Triggers:**
- After completing any implementation that changes system behavior
- When brief explicitly requires documentation updates
- When code changes affect user-facing functionality

**Process:**
1. Update header (version + date) FIRST
2. Make content changes
3. Verify all required sections updated
4. Ensure consistency with existing documentation style

### THINKING_BUDDY

**Responsible for:**
- Creating briefs (which become documentation artifacts)
- Updating `docs/USER_GUIDE.md` when introducing new workflows (in coordination with CB)
- Updating agent specifications if role boundaries change significantly
- Ensuring briefs are complete and will result in proper documentation

**Update Triggers:**
- Creating briefs for new workflows or significant changes
- When agent specifications need clarification or updates
- When framework documentation needs structural changes

### CONTEXT_STEWARD

**Responsible for:**
- Updating documentation files to clarify context or adapt the framework
- Updating agent specifications to clarify roles or adapt the framework
- Updating framework documentation (`docs/WORKFLOW.md`, `docs/QUALITY_STANDARDS.md`, etc.) when helping users adapt toolkit
- **NEVER writes code or modifies project deliverables**

**Update Triggers:**
- When clarifying context requires documentation updates
- When adapting framework requires documentation changes
- When explaining framework usage reveals documentation gaps

**Process:**
- Follow same header update rules (version + date)
- Focus on clarity and accuracy
- Maintain consistency with existing documentation

### SYSTEM_BUDDY

**Responsible for:**
- **NOT directly updating documentation** (creates findings instead)
- Identifying documentation drift and gaps in findings
- Recommending documentation updates via findings → TB → CB workflow
- Validating documentation freshness during reviews

**Process:**
- Document documentation issues in findings
- Route to TB for brief creation if documentation updates needed
- Never directly modify documentation files

---

## Documentation Update Rules by Document Type

### `docs/system/SYSTEM_SUMMARY.md`

**When to update:** After ANY system change (behavior, architecture, workflow, agent behavior)

**Updated by:** CODING_BUDDY (after implementation)

**Required Updates:**
1. **Changelog entry** (add to top of changelog section):
   ```markdown
   ## [Version] - YYYY-MM-DD
   
   **Status:** [Enhancement | Fix | Redesign | Breaking]
   
   **What Changed:** [Brief summary - concise, high-level]
   
   **Brief Reference:**
   - Brief: `work/briefs/archive/YYYY-MM-DD_name_brief.md`
   - For detailed implementation context, decisions, and rationale, see the brief (brief is archived after implementation)
   
   **System-Level Decisions:** (Only if brief contains "System-Level Decisions" section)
   - Decision: [What system-level decision was made - extract from brief]
   - Trade-off: [What was considered - extract from brief]
   - Rationale: [Why this decision - extract from brief]
   - Impact: [How this affects system architecture/patterns/future work - extract from brief]
   
   **Impact:** [What this affects - users, agents, workflows, system architecture, etc.]
   
   **Files Modified:** [List of files changed]
   ```
   
   **Extraction Rules:**
   - If brief has "System-Level Decisions" section: Extract decisions, trade-offs, and rationale to SYSTEM_SUMMARY changelog entry
   - If brief does NOT have system-level decisions: Omit "System-Level Decisions" section or state: "No system-level decisions - standard implementation"
   - Always include brief reference for detailed implementation context
   - Briefs contain detailed "what" and "why" - SYSTEM_SUMMARY focuses on system-wide impact and architectural decisions

2. **Relevant sections:** Update system behavior descriptions, architecture diagrams, workflow descriptions if changed

3. **Header:** Update version and date

**Quality Checks:**
- Changelog entry is clear and complete
- Sections accurately reflect current state
- Version and date are current

### `docs/USER_GUIDE.md`

**When to update:** 
- New workflows introduced
- System architecture changes that affect users
- Agent behavior changes that affect user interactions
- Documentation structure changes

**Updated by:** TB (when creating briefs for new workflows) or CB (when implementation changes user-facing behavior)

**Required Updates:**
1. **Relevant sections:** Update or add sections as needed
2. **Table of Contents:** Add new sections if structure changes
3. **Cross-references:** Update links if file structure changes
4. **Header:** Update version and date

**Quality Checks:**
- Content reflects actual current behavior
- Formatting is consistent
- Examples are accurate
- Table of Contents is current

### Agent Specifications (`docs/agents/*.md`)

**When to update:**
- Agent behavior changes
- Role boundaries change
- New responsibilities added
- Clarifications needed

**Updated by:** TB (when role changes are defined) or CONTEXT_STEWARD (when clarifying roles) or CB (when implementing role changes)

**Required Updates:**
1. **Relevant sections:** Update behavior descriptions, boundaries, responsibilities
2. **Version history:** Consider adding version history section for significant changes
3. **Cross-references:** Update references to other agents if boundaries change
4. **Header:** Update version and date

**Quality Checks:**
- Role boundaries are clear
- Responsibilities don't overlap inappropriately
- Examples are accurate
- Cross-references are current

### System Prompts (`docs/prompts/*.txt`)

**When to update:**
- Roles change significantly
- Prompt effectiveness issues identified
- New behaviors need enforcement
- Prompt structure needs improvement

**Updated by:** TB or operator (prompt design) or CB (if implementing prompt changes)

**Required Updates:**
1. **Prompt content:** Update instructions as needed
2. **Version header:** If prompts have version headers, update them
3. **Agent spec alignment:** Ensure agent spec reflects prompt changes
4. **Documentation:** Update SYSTEM_SUMMARY changelog if prompt changes affect behavior

**Quality Checks:**
- Prompts clearly communicate role and boundaries
- Prompts align with agent specifications
- Prompt changes are documented

### Root `README.md`

**When to update:**
- Framework structure changes
- Setup process changes
- New major features added
- Agent descriptions change significantly

**Updated by:** CB (after implementation) or TB (when structure changes)

**Required Updates:**
1. **Structure diagram:** Update if directory structure changes
2. **Setup instructions:** Update if setup process changes
3. **Agent descriptions:** Update if roles or capabilities change significantly
4. **Quick start:** Update if initial setup changes
5. **Header:** Update version and date if framework version is tracked

**Quality Checks:**
- Structure diagram is accurate
- Setup instructions work
- Agent descriptions are current
- Links are valid

### Framework Documentation (`docs/*.md`)

**When to update:**
- Framework rules or workflows change
- New standards are introduced
- Clarifications needed based on usage

**Updated by:** TB, CONTEXT_STEWARD, or CB (depending on change type)

**Required Updates:**
1. **Content:** Update relevant sections
2. **Header:** Update version and date
3. **Cross-references:** Update if referenced documents change

**Quality Checks:**
- Content is accurate and current
- Examples are relevant
- Cross-references are valid

---

## Documentation Quality Standards

### Content Quality

**Accuracy:**
- Documentation must accurately describe current behavior
- Examples must work with current system
- Instructions must be correct and complete

**Completeness:**
- All required information is present
- No critical information is missing
- Sections are complete, not placeholder content

**Clarity:**
- Language is clear and unambiguous
- Technical terms are defined when first used
- Examples illustrate concepts effectively

**Consistency:**
- Terminology is consistent across all documentation
- Formatting follows established patterns
- Style is consistent

### Formatting Standards

**Markdown:**
- Use standard Markdown syntax
- Headers follow hierarchy (H1 for title, H2 for main sections, H3 for subsections)
- Lists are properly formatted
- Code blocks have language specified when relevant
- Links are descriptive (not "click here")

**Structure:**
- Logical organization with clear sections
- Table of Contents for long documents
- Consistent section ordering where applicable
- Clear headings that describe content

**Readability:**
- Appropriate line length (wrap at reasonable length)
- White space for visual separation
- Bullet points for lists
- Tables for structured data

### Version and Date Management

**MANDATORY RULES:**
1. **Always update version and date** when modifying documentation
2. **Update BEFORE or DURING edit**, not after
3. **Use semantic versioning** (major.minor.patch)
4. **Use ISO 8601 date format** (YYYY-MM-DD)
5. **Be consistent** with version increment decisions

**Version Increment Guidelines:**
- **Patch (1.0 → 1.0.1):** Typos, formatting, minor clarifications
- **Minor (1.0 → 1.1):** New sections, significant additions, non-breaking changes
- **Major (1.0 → 2.0):** Structural changes, breaking format changes, major rewrites

---

## Maintenance Triggers and Processes

### Automatic Triggers (MANDATORY)

**After Implementation (CB):**
1. System behavior changed → Update `SYSTEM_SUMMARY.md` changelog
2. User-facing behavior changed → Update `USER_GUIDE.md`
3. Framework structure changed → Update `README.md` structure diagram

**During Brief Creation (TB):**
1. New workflow → Plan `USER_GUIDE.md` updates in brief
2. Agent role changes → Plan agent spec updates in brief

**During Context Clarification (CONTEXT_STEWARD):**
1. Documentation gap identified → Update relevant documentation
2. Framework adaptation needed → Update framework docs

### Periodic Maintenance (SYSTEM_BUDDY)

**Context Integrity Reviews:**
- Check documentation freshness (version/date)
- Compare documentation to actual behavior
- Identify documentation drift
- Recommend updates via findings

**Review Frequency:**
- Weekly light review: Quick check for obvious issues
- Monthly deep review: Comprehensive documentation audit

### Manual Triggers

**User requests:**
- User identifies documentation issue → Route to appropriate agent
- User requests documentation update → Create brief (TB) or direct update (if appropriate)

**Agent identifies gap:**
- Agent notices documentation is outdated → Update (if within scope) or create finding (if outside scope)

---

## Cross-Reference Management

### Internal Links

**When creating links between documents:**
- Use relative paths: `[Link Text](../relative/path/to/file.md)`
- Ensure links are descriptive (not "click here")
- Verify links are valid and point to correct sections
- Update links when files are moved or renamed

### External References

**When referencing external resources:**
- Use full URLs for external links
- Include title/description of external resource
- Note if external resource may change or become unavailable
- Consider archiving critical external references

### Link Maintenance

**When updating documentation:**
- Check all links in the document are valid
- Update links if referenced documents moved
- Fix broken links immediately
- Verify anchor links work (for section references)

---

## Documentation Review and Validation

### Self-Check (Before Finalizing)

**For all documentation updates, verify:**
1. ✅ Header updated (version + date)
2. ✅ Content is accurate and current
3. ✅ Formatting is consistent
4. ✅ Links are valid
5. ✅ Examples work (if applicable)
6. ✅ Terminology is consistent
7. ✅ No placeholder content
8. ✅ Required sections are complete

### Peer Review (When Appropriate)

**For significant documentation changes:**
- Have another agent review for accuracy
- Check cross-references in other documents
- Verify examples and instructions work
- Ensure consistency with related documentation

### SYSTEM_BUDDY Validation

**During context integrity reviews:**
- Check version/date currency
- Compare documentation to actual behavior
- Identify inconsistencies
- Verify cross-references
- Check for documentation drift

---

## Special Cases and Exceptions

### READ-ONLY Documentation

**`docs/project-context/` folder:**
- **DO NOT UPDATE** unless explicitly requested by user in brief
- These files are maintained by the user, not agents
- Reference for understanding, but do not modify
- Exception: If brief explicitly requests update, CB may update (but still follows version/date rules)

**Example files (`*-EXAMPLE.md`):**
- **DO NOT UPDATE** - These are templates/placeholders
- Agents should ignore these files
- These are maintained by framework, not project-specific

### Templates

**Template files (`docs/briefs/*-template.md`):**
- Templates are framework documentation files
- **MUST have version/date headers** like other documentation
- Template content (inside the file) may have template-specific formats (e.g., Date, Created By, Status for briefs)
- Templates are versioned as framework documentation, not as instances
- When templates are updated, version and date must be updated in template file header

### Temporary Documentation

**Briefs and Findings:**
- Located in `work/briefs/` and `work/findings/`
- Follow same version/date standards if they have headers
- These are working documents but still benefit from standards
- Instances created from templates don't need to follow template versioning (they use their own date/status)

### Code Comments and Inline Documentation

**Code-level documentation:**
- Follow language-specific documentation standards
- Keep comments current with code
- Update when code changes
- Use appropriate documentation generation tools if applicable

---

## Enforcement and Accountability

### Agent Accountability

**Each agent is responsible for:**
- Following these standards in their own work
- Identifying documentation issues in their domain
- Updating documentation when they make changes
- Maintaining quality in their documentation updates

### Violation Consequences

**Documentation without current version/date:**
- Misleads users about document currency
- Violates trust in documentation system
- Creates context drift risk
- Must be corrected immediately

### Quality Gates

**Before closing any work that affects documentation:**
- Verify documentation is updated if needed
- Verify version and date are current
- Verify content is accurate
- Verify links and cross-references are valid

---

## Best Practices

### Do's

✅ **DO** update documentation as part of implementation, not as separate task  
✅ **DO** update header (version + date) first, then content  
✅ **DO** verify accuracy before finalizing  
✅ **DO** maintain consistency with existing documentation style  
✅ **DO** check cross-references when updating  
✅ **DO** use clear, descriptive language  
✅ **DO** include examples where helpful  
✅ **DO** keep examples current and working  

### Don'ts

❌ **DON'T** update documentation without updating version/date  
❌ **DON'T** leave placeholder content  
❌ **DON'T** create broken links  
❌ **DON'T** use outdated examples  
❌ **DON'T** assume documentation is current without checking  
❌ **DON'T** skip documentation updates to save time  
❌ **DON'T** document aspirational behavior instead of actual behavior  
❌ **DON'T** create documentation that conflicts with other documentation  

---

## Quick Reference Checklist

**When updating ANY documentation file:**

- [ ] Update version number (major.minor.patch)
- [ ] Update date (YYYY-MM-DD format)
- [ ] Update header BEFORE or DURING edit
- [ ] Verify content is accurate and current
- [ ] Check formatting consistency
- [ ] Verify all links are valid
- [ ] Check cross-references
- [ ] Ensure terminology is consistent
- [ ] Remove any placeholder content
- [ ] Complete all required sections
- [ ] Verify examples work (if applicable)
- [ ] Self-check before finalizing

---

**Remember:** Documentation is a living part of the system. It must evolve with the system and remain accurate, current, and useful. Following these standards ensures documentation serves its critical role in context management.

