# Project Context Folder

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** READ-ONLY project-specific context and domain knowledge

---

## ⚠️ READ-ONLY FOLDER

**This folder contains READ-ONLY reference material. Agents will NOT maintain or update files in this folder unless explicitly asked.**

### Rules for Agents

- **READ:** Agents may read files in this folder to understand project context, business rules, domain knowledge, and requirements
- **DO NOT WRITE:** Agents must NOT automatically update, modify, or maintain files in this folder
- **EXPLICIT PERMISSION REQUIRED:** Agents may only update files in this folder when explicitly requested by the user (e.g., in a brief or task)

### Rules for Users

- **You maintain this folder:** Add, update, or remove files as your project context evolves
- **Keep it current:** Since agents won't automatically update these files, ensure they reflect current project reality
- **Explicit updates:** If you want agents to update files here, explicitly request it (e.g., "Update `docs/project-context/domain-requirements.md` with the new business rule about X")
- **Example file:** `domain-requirements-EXAMPLE.md` is a template showing the structure - create your own `domain-requirements.md` file

---

## Purpose

This folder stores project-specific domain knowledge, business rules, requirements, and contextual information that agents need to understand your project.

### What to Store Here

- **Domain requirements and business rules** - Business logic, domain-specific terminology, compliance requirements
- **Project specifications** - API contracts, integration requirements, third-party service documentation  
- **Business context** - Target users, business model, success metrics, roadmap information
- **Reference materials** - Requirements documents, design specifications, stakeholder notes (as PDF, DOCX, or Markdown)

### File Formats

- **Preferred:** Markdown (`.md`) files - Agents can read these directly
- **Supported:** PDF (`.pdf`) and DOCX (`.docx`) files - Agents can extract text from these formats
- **Organization:** Organize files by topic (e.g., `domain-requirements.md`, `api-specifications.md`, `integration-docs.pdf`)

---

## Example Files

**⚠️ IMPORTANT:** The file `domain-requirements-EXAMPLE.md` contains EXAMPLE/PLACEHOLDER content about "Acme Webshop". This is NOT real project context.

- **This is a template** showing what type of content belongs in project-context files
- **The "-EXAMPLE" suffix makes it clear this is example data** - agents should ignore it until you create your own project-context files
- **Do NOT use this example data** - agents should ignore it until you create your actual project context files
- **You can delete this example file** once you've created your own project-context files
- **Agents should NOT reference "Acme Webshop"** or any other placeholder content - it's example data only

**Before agents read project-context files:**
1. Create your own `domain-requirements.md` (or similar) with your actual project's domain requirements, OR
2. Delete the example file and create your own project-context files

Only files with your actual project information should be treated as authoritative project context. Files with "-EXAMPLE" suffix are templates only.

---

## Notes

- Files in this folder are treated as authoritative reference sources
- Agents consult these files to inform decisions and understand constraints
- Files remain static unless you explicitly request agent updates
- Keep files current manually, or explicitly request agent updates when context changes

