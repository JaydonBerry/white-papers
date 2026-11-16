---
title: "Defining Production-Ready Across Teams"
id: WP-0004
status: draft
version: 1.0.0
authors: ["Jaydon Berry"]
created: 2026-11-13
updated: 2026-11-13
audience: [mid-level, senior, staff, architect, engineering-manager, director]
tags: [production-readiness, reliability, security, testing, release-governance]
summary: "Defines a common production-readiness gate so software teams release with consistent quality, security, and operational controls."
supersedes: []
related: [WP-0002, WP-0003]
---

# WP-0004: Defining Production-Ready Across Teams

## Abstract
"Done" is insufficient for reliable delivery at a scale that encompasses multiple teams with differing practices and cultures. 
This paper defines a common production-readiness framework with explicit release criteria.

## Motivation
Without a shared definition of production readiness, teams release software with inconsistent test depth, weak observability, and incomplete rollback plans. These gaps drive incident volume, increase change failure rates, and reduce trust between engineering and business stakeholders. Where cross-team release decisions are required, a common production-readiness definition enables consistent quality, security, and operational controls.

## Specification
1. A release candidate MUST satisfy all required controls in five domains: Security, Testing, Observability, Operability, and Documentation.
	- Security controls MUST include dependency scanning and remediation of critical vulnerabilities before production deployment.
	- Testing controls MUST include automated tests for critical paths and a passing CI quality gate.
	- Observability controls MUST include structured logging, service-level metrics, and actionable alerts for critical failure modes.
	- Operability controls MUST include a validated rollback or forward-fix procedure.
	- Documentation controls MUST include an owner, service overview, and operational runbook.
2. Any release that fails a MUST control MUST NOT be promoted without formal risk acceptance from a designated approver.
3. Teams SHOULD define additional SHOULD controls based on service tier, customer impact, and regulatory scope.
4. Readiness checks SHOULD be automated in CI/CD to reduce manual variance.
5. Teams MAY maintain service-specific readiness extensions if they do not weaken baseline controls.

## Examples
### Baseline Production-Readiness Checklist
- Security: Critical vulnerabilities resolved or explicitly risk-accepted.
- Testing: Critical-path integration tests passing.
- Observability: Error rate, latency, and throughput dashboards available.
- Operability: Rollback procedure tested in a non-production environment.
- Documentation: Runbook linked in service metadata.

### Release Decision Example
A release with failed rollback verification does not meet a MUST requirement and MUST remain blocked until rollback verification passes or formal risk acceptance is recorded. If the release is approved with risk acceptance, the approver MUST document the rationale and mitigation plan in the release notes. Then the release CAN be promoted to production, but the team MUST remediate the rollback gap within a defined timeframe.

## Rationale and Alternatives
A single baseline across teams reduces subjective release decisions and simplifies leadership reporting. A fully decentralized model was considered but rejected because inconsistent criteria make organization-wide reliability management difficult. In a group of teams with decentralized diverse practices, release decisions can be difficult to audit and can erode trust between teams.

## Security and Operational Considerations
1. Risk-acceptance pathways can be abused; approvals SHOULD be limited to authorized leadership roles.
2. Manual checklists can produce false confidence; controls SHOULD be validated by automated evidence where possible.
3. Control definitions SHOULD be reviewed periodically to prevent stale criteria and checklist drift.

## References
- RFC 2119: Key words for use in RFCs to Indicate Requirement Levels — https://www.rfc-editor.org/info/rfc2119