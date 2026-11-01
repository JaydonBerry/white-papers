---
title: "White Paper Format: RFC-Style Markdown with YAML Frontmatter"
id: WP-0001
status: accepted
version: 1.0.0
authors: ["JaydonBerry"]
created: 2026-11-01
updated: 2026-11-01
audience: [junior, mid-level]
tags: [meta, documentation, format, portability]
summary: "Defines the RFC-style Markdown layout and YAML metadata header used by every white paper in this repository."
supersedes: []
related: []
---

# WP-0001: White Paper Format

## Abstract
Every paper is a plain Markdown file with a YAML frontmatter header and RFC-style sections. Markdown and YAML frontmatter are parsed natively by GitHub Copilot, Obsidian, Logseq and vector-database ingestion pipelines, so the repository can be dropped into any second-brain system without conversion.

## Specification
1. Papers MUST live in `papers/` and be named `WP-NNNN-slug.md`.
2. Papers MUST begin with the YAML frontmatter shown in `templates/WHITE-PAPER-TEMPLATE.md`.
3. Papers SHOULD use the template's sections: Abstract, Motivation, Specification, Examples, Rationale and Alternatives, Security and Operational Considerations, References.
4. Requirements SHOULD use RFC 2119 keywords (MUST, SHOULD, MAY).
5. Papers MUST NOT depend on tool-specific syntax; use standard Markdown and relative links.

## Rationale and Alternatives
Plain text avoids lock-in; frontmatter gives machines structured metadata (`tags`, `summary`, `status`) while the body stays readable for humans.
