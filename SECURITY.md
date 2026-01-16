# Security Policy

This document describes how to report security issues in the KDF specification.

---

## Scope

Security issues in the KDF specification include:

- **Specification ambiguity** that could lead to inconsistent implementations
- **Forgery risk** where artifacts could be constructed to falsely claim validity
- **Hash collision concerns** affecting source or fingerprint integrity
- **Validation bypass** where non-compliant artifacts could pass conformance

Security issues do NOT include:

- Bugs in specific implementations (report to that implementation's repository)
- Extraction quality or AI behavior (out of scope for KDF)
- Feature requests or scope expansions

---

## How to Report

For security-sensitive issues, email the maintainers directly rather than opening a public issue.

**Contact:** Open a private security advisory via GitHub's Security tab, or email the repository owner listed in GOVERNANCE.md.

Include:

1. Description of the issue
2. Affected specification sections
3. Potential impact
4. Suggested remediation (if any)

---

## Response Process

1. **Acknowledgment:** We aim to acknowledge reports within 7 days
2. **Assessment:** We will assess severity and affected versions
3. **Remediation:** Specification clarifications will be drafted
4. **Disclosure:** Coordinated disclosure after remediation is published

---

## Expectations

- No SLAs are provided; this is a volunteer-maintained project
- We prioritize specification clarity over speed
- Minor ambiguities may be addressed in regular releases
- Critical issues will be prioritized

---

## Related Documents

- [THREAT_MODEL.md](spec/THREAT_MODEL.md) — Security guarantees and non-guarantees
- [SUPPORT.md](SUPPORT.md) — General support expectations
