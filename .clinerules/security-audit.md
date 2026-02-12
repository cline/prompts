---
description: "Guides Cline to perform structured security audits — covering OWASP Top 10, threat modeling, dependency scanning, secrets detection, and compliance-aware reporting."
author: "Cline Team"
version: "1.0"
category: "Development"
tags: ["security", "audit", "owasp", "threat-modeling", "vulnerability", "compliance"]
globs: ["*.*"]
---

# Security Audit & Threat Modeling Protocol

## Objective

Guide Cline to perform thorough, structured security assessments of codebases. This goes beyond the surface-level checks in code review — it provides a repeatable methodology for identifying vulnerabilities, assessing risk, and producing actionable remediation plans.

---

## When to Activate

This protocol activates when the user requests:
- A security audit or review
- Threat modeling for a feature or system
- Dependency vulnerability analysis
- Pre-deployment security checks
- Compliance-related code assessment

---

## 1. Security Audit Process

### Phase 1: Reconnaissance

Before analyzing code, gather context:

1. **Identify the attack surface** — What is exposed? (APIs, user inputs, file uploads, auth endpoints, admin panels)
2. **Identify trust boundaries** — Where does data cross from untrusted to trusted zones?
3. **Identify sensitive data** — PII, credentials, tokens, financial data, health records
4. **Identify dependencies** — Third-party libraries, external services, infrastructure

### Phase 2: Systematic Analysis

Analyze the codebase against these categories, ordered by typical severity:

#### A. Injection Flaws (OWASP A03)
- SQL injection via string concatenation or unsanitized ORM inputs
- Command injection via `exec`, `system`, `child_process`, or `subprocess`
- LDAP, XPath, NoSQL injection vectors
- Template injection in server-side rendering

**What to check:**
```
- [ ] All database queries use parameterized statements or prepared queries
- [ ] No user input is passed directly to shell commands
- [ ] Template engines have auto-escaping enabled
- [ ] ORM queries do not interpolate raw user input
```

#### B. Authentication & Session Management (OWASP A07)
- Password storage (must use bcrypt, scrypt, or argon2 — never MD5/SHA1 alone)
- Session token generation (must be cryptographically random)
- Token expiration and rotation policies
- Multi-factor authentication implementation
- Account lockout and brute-force protection

**What to check:**
```
- [ ] Passwords hashed with a modern, salted algorithm
- [ ] Session tokens are not predictable
- [ ] JWT secrets are not hardcoded and tokens have expiration
- [ ] Failed login attempts are rate-limited
- [ ] Password reset flows do not leak user existence
```

#### C. Authorization & Access Control (OWASP A01)
- Broken access control (IDOR — insecure direct object references)
- Missing function-level access checks
- Privilege escalation paths
- CORS misconfiguration

**What to check:**
```
- [ ] Every endpoint enforces authorization, not just authentication
- [ ] Object-level access checks prevent users from accessing other users' data
- [ ] Admin functions are not accessible by manipulating client-side state
- [ ] CORS allows only expected origins
```

#### D. Sensitive Data Exposure (OWASP A02)
- Secrets in source code (API keys, passwords, tokens)
- Sensitive data in logs
- Missing encryption for data at rest or in transit
- Overly verbose error messages leaking internals

**What to check:**
```
- [ ] No secrets or credentials in source files or config committed to git
- [ ] Sensitive fields are excluded from logs and error responses
- [ ] HTTPS is enforced; no mixed content
- [ ] Database connections use TLS
- [ ] Error responses do not expose stack traces or internal paths
```

#### E. Cross-Site Scripting — XSS (OWASP A03)
- Reflected XSS via URL parameters rendered without escaping
- Stored XSS via database content rendered in HTML
- DOM-based XSS via client-side JavaScript

**What to check:**
```
- [ ] All user-generated content is escaped before rendering
- [ ] Content-Security-Policy headers are configured
- [ ] innerHTML is not used with untrusted data
- [ ] Rich text inputs use a sanitization library (e.g., DOMPurify)
```

#### F. Dependency Vulnerabilities (OWASP A06)
- Known CVEs in direct and transitive dependencies
- Outdated packages with security patches available
- Typosquatting or supply chain risks

**What to check:**
```
- [ ] `npm audit` / `pip audit` / `dotnet list package --vulnerable` has been run
- [ ] No dependencies with known critical/high CVEs
- [ ] Lock files are committed and reviewed
- [ ] Dependency update process exists
```

### Phase 3: Secrets Detection

Scan for accidentally committed secrets:

**Patterns to search for:**
- API keys: `(api[_-]?key|apikey)\s*[:=]\s*['"][A-Za-z0-9]`
- AWS keys: `AKIA[0-9A-Z]{16}`
- Generic secrets: `(password|secret|token)\s*[:=]\s*['"][^'"]+`
- Private keys: `-----BEGIN (RSA |EC |)PRIVATE KEY-----`
- Connection strings: `(mongodb|postgres|mysql|redis):\/\/[^\s]+`

**MUST** use `search_files` to scan the codebase for these patterns when performing a security audit.

---

## 2. Threat Modeling (STRIDE)

When asked to threat-model a feature or system, apply the STRIDE framework:

| Threat | Question | Example |
|--------|----------|---------|
| **S**poofing | Can someone pretend to be another user or system? | Forged JWT, session hijacking |
| **T**ampering | Can someone modify data they should not? | URL parameter manipulation, unsigned API payloads |
| **R**epudiation | Can someone deny an action they took? | Missing audit logs for admin actions |
| **I**nformation Disclosure | Can someone access data they should not see? | IDOR, verbose errors, exposed .env files |
| **D**enial of Service | Can someone make the system unavailable? | Unbounded queries, missing rate limits, regex DoS |
| **E**levation of Privilege | Can someone gain higher access than intended? | Missing role checks, JWT claim manipulation |

**Output format:** Present findings as a table mapping each threat to specific code locations and recommended mitigations.

---

## 3. Output Format

Present audit findings grouped by severity:

**CRITICAL** — Exploitable now, data loss or breach risk
- Must be fixed before deployment

**HIGH** — Likely exploitable with moderate effort
- Should be fixed in the current sprint

**MEDIUM** — Exploitable under specific conditions
- Should be tracked and scheduled

**LOW** — Defense-in-depth improvements
- Nice to have, fix opportunistically

For each finding:
1. **Location** — File and line/section
2. **Vulnerability** — What the issue is
3. **Risk** — What could happen if exploited
4. **Remediation** — Specific fix with code example when possible
5. **Reference** — OWASP or CWE identifier if applicable

End with an executive summary: total findings by severity, top 3 priorities, and overall security posture assessment.

---

## 4. Pre-Completion Security Checklist

Before `attempt_completion` on any security-related task:

- [ ] All OWASP Top 10 categories have been evaluated
- [ ] Secrets scan has been performed
- [ ] Findings are categorized by severity
- [ ] Each finding has a concrete remediation
- [ ] Executive summary is included

<!--
Enterprise Considerations:
- Organizational security policy templates aligned to SOC2, HIPAA, PCI-DSS
- Centralized vulnerability tracking and trend analysis across repositories
- Automated audit trail generation for compliance evidence packages
- Admin-configurable severity thresholds that block deployments
- Integration with enterprise SIEM and vulnerability management platforms
-->
