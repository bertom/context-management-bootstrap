# Project Context File

**Version:** 1.0  
**Last Updated:** 2026-01-09  
**Purpose:** Example file showing where to store project-specific context

---

## ⚠️ THIS IS AN EXAMPLE FILE

**This file has "-EXAMPLE" suffix and can be safely deleted.**

- **This folder (`docs/project-context/`) is for storing all your project-specific context**
- Store any project context here: domain knowledge, business rules, requirements, API specifications, etc.
- Files in this folder are READ-ONLY by default - agents will not modify them unless explicitly asked
- You can organize files however you want (e.g., `domain-requirements.md`, `api-specifications.md`, `business-rules.md`)
- Supported formats: Markdown (`.md`) preferred, PDF (`.pdf`) and DOCX (`.docx`) also supported

**This example file is just a placeholder - delete it and create your own project-context files as needed.**

---

## Notes

- Files with "-EXAMPLE" suffix are templates only - agents will ignore them
- Agents read files in this folder to understand project context, business rules, and domain knowledge
- Keep your project-context files current - agents won't automatically update them
- If you want agents to update project-context files, explicitly request it in a brief or task
