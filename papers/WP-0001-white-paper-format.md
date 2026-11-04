---
title: "White Paper Format: RFC-Style Markdown with YAML Frontmatter"
id: WP-0001
status: accepted
version: 1.0.0
authors: ["Jaydon Berry"]
created: 2026-11-01
updated: 2026-11-01
audience: [junior, mid-level]
tags: [standards, documentation, format, portability]
summary: "Defines the RFC-style Markdown layout and YAML metadata header used by every white paper in this repository."
supersedes: []
related: []
---

# WP-0001: White Paper Format using RFC 2119-style Markdown with YAML Frontmatter

## Abstract
Every paper is a plain Markdown file with a YAML frontmatter header and RFC-style sections. 
Markdown and YAML frontmatter are parsed natively by GitHub Copilot, Obsidian, Logseq and vector-database ingestion pipelines, so the repository can be dropped into any second-brain system without conversion.

## Specification

This paper uses RFC 2119 keywords to express the strength of authoring rules in this document (not to define a separate template section):

- **MUST / SHALL / REQUIRED**: Absolute requirement. No deviation allowed.
- **MUST NOT / SHALL NOT**: Absolute prohibition. Never allowed.
- **SHOULD / RECOMMENDED**: Strong recommendation. Follow unless there is a valid, well-understood reason not to.
- **SHOULD NOT**: Strong discouragement. Avoid unless there is a valid, well-understood reason to do it.
- **MAY / OPTIONAL**: Truly optional. Choice is left to the implementer.

### Repository Structure
1. Papers MUST live in `papers/` and be named `WP-NNNN-White.md`.
2. Papers MUST begin with the YAML frontmatter shown in `templates/WHITE-PAPER-TEMPLATE.md`.
3. Papers SHOULD use the template's sections: 
	1. Abstract
	2. Motivation 
	3. Specification 
	4. Examples
	5. Rationale
	6. Alternatives
	7. Security and Operational Considerations
	8. References
4. Statements that define requirements in this specification SHOULD use RFC 2119 keywords (MUST, SHOULD, MAY).
5. Papers MUST NOT depend on tool-specific syntax; use standard Markdown and relative links.

## Rationale and Alternatives
Plain text avoids lock-in, where an institution's knowledge could be trapped in a proprietary format or platform; 
frontmatter gives machines structured metadata (`tags`, `summary`, `status`) while the body stays readable for humans, allowing for dual use between providing context for AI-assisted tools and being a human-readable document.

## References
https://www.rfc-editor.org/info/rfc2119/