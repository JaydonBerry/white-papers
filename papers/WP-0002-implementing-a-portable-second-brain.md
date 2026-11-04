---
title: "Implementing a Portable Second Brain"
id: WP-0002
status: accepted
version: 1.1.0
authors: ["Jaydon Berry"]
created: 2026-11-01
updated: 2026-11-04
audience: [junior, mid-level, senior, architect]
tags: [standards, documentation, format, portability]
summary: "Defines a portable second brain (context repository) structure and how projects should consume it through a context root file."
supersedes: []
related: []
---

# WP-0002: Implementing a Portable Second Brain

## Abstract
A "second brain" is a plain-text context repository designed to be portable, machine-readable, and human-readable.
This paper defines a practical folder hierarchy that improves consistency for AI-assisted development tools while remaining easy for humans to review, edit, and govern.

## Motivation
AI-assisted engineering is now common, but tool providers, models, and workflows change frequently. Teams need a durable way to preserve operational knowledge, architecture decisions, and coding rules without locking that knowledge into one vendor format.

A repository-based context approach keeps humans in control, supports peer review through source control, and allows teams to reuse the same knowledge across tools such as Copilot and other assistants.

## Specification
1. The repository MUST remain plain-text and self-contained so it can be hot dropped into another location without build or conversion steps.
2. Content MUST use standard Markdown and YAML frontmatter only; tool-specific extensions SHOULD be avoided.
3. Internal links MUST be relative links so documents remain valid after moving the folder.
4. Metadata fields (`id`, `title`, `summary`, `tags`, `status`) SHOULD be present and consistent to improve retrieval quality in AI tools.
5. Context files SHOULD be organized as a standalone repository in a stable location (for example `C:/context/`) so multiple projects can reference the same knowledge base.
6. A **context root** is the top-level instruction Markdown file stored inside a project directory that points to and governs use of the shared context repository.
7. The context repository SHOULD include reusable prompt patterns, architecture documentation, and coding standards so AI agents can make better implementation decisions.
8. Any `.md` file MAY evolve into a folder with subfolders as content grows, but the context repository itself MUST remain a single portable folder.


## Examples
Example portable "second brain" layout:

```text
C:/context/
├── .github/
│   └── copilot-instructions.md
├── 0-inbox/
├── 1-product-definitions/
│   ├── core-banking-service.md
│   └── developer-portal.md
├── 2-implementation-plans/
│   ├── active-sprints/
│   └── system-rules/
├── 3-architecture/
│   ├── greenfield-blueprints/
│   ├── existing-software/
│   │   ├── legacy-payment-monolith.md
│   │   └── inventory-worker-v1.md
│   └── cross-cutting/
│       └── open-telemetry-spec.md
└── 4-rules-and-best-practices/
    ├── software-rules/
    │   ├── async-await-standards.md
    │   └── dependency-injection.md
    └── data-rules/
        ├── ef-core-best-practices.md
        └── schema-migrations.md
```

Example project reference file:
````markdown
# GitHub Copilot Instructions

Use the shared second brain at `C:/context/` as the project's external context repository.

## 1. Context Mapping
Reference these folders as the primary context sources:
- `1-product-definitions/` (product specs)
- `2-implementation-plans/` (tactical plans and system rules)
- `3-architecture/` (architecture standards and system constraints)
- `4-rules-and-best-practices/` (software and data rules)

## 2. Core Rules

### Rule A: Honor Existing Software Constraints
- If work is scoped to `/3-architecture/existing-software/`, keep solutions backward-compatible with the documented stack.
- Do not propose greenfield-only features for legacy systems unless the user explicitly requests migration guidance.

### Rule B: Enforce Code vs. Data Bifurcation
- **C# logic rules (`/4-rules-and-best-practices/software-rules/`):** prefer non-blocking `async`/`await`; avoid `.Result` and `.Wait()`; use modern C# only when the target runtime supports it.
- **Data rules (`/4-rules-and-best-practices/data-rules/`):** use non-tracking reads when appropriate, keep filtering/pagination/projection in the database, and follow zero-downtime migration rules.

### Rule C: Architectural Attribution
- When making a major architectural recommendation, cite the exact rule that mandates it.
- *Example:* "I used a scoped lifetime here to prevent state leaks across HTTP requests, as mandated by `[Dependency Injection Rules](../../4-rules-and-best-practices/software-rules/dependency-injection.md)`."

````

This layout is designed for ingestion by many AI tools while keeping a consistent, reviewable context source. Any Markdown file in the second brain repository can be referenced from a project's context root file, and the repository can be relocated with minimal changes because links remain relative.

## Rationale and Alternatives
This approach was selected after comparing three patterns:

- Agent-pipeline-heavy approaches, which can produce strong automation but add operational complexity.
- Prompt-only approaches, which are fast to start but difficult to scale consistently across teams.
- Repository-based context engineering, which requires ongoing curation but is portable, auditable, and reusable.

Given portability, readability, and governance requirements, the repository-based approach is preferred. Source control provides change history, review workflows, and accountability for context quality.

## Security and Operational Considerations
1. The context repository and project context roots may include sensitive information. Access control, secret handling policies, and sharing boundaries MUST be enforced.
2. Context quality decays without ownership. Teams SHOULD define maintainers, review cadence, and archival rules.
3. Very large repositories may reduce tool responsiveness. Teams SHOULD prune obsolete files and prefer focused references from each context root.
4. Adoption requires onboarding. Teams SHOULD train developers on how to create, reference, and maintain context consistently.

## References
- Microsoft Learn: Prompt engineering techniques with Azure OpenAI — https://learn.microsoft.com/azure/ai-services/openai/concepts/prompt-engineering
- GitHub Docs (GitHub Copilot): Adding repository custom instructions — https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot
- GitHub Docs (GitHub Copilot): About personal custom instructions — https://docs.github.com/en/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
