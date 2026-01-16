# Support

This document sets expectations for support and contributions.

---

## What This Project Provides

- A normative specification for KDF artifacts
- Conformance fixtures for validator implementations
- Documentation for adoption and integration
- A reference validator (in the `kdf-validator` repository)

---

## What This Project Does NOT Provide

- Hosted validation services
- Extraction pipelines or tooling
- Consulting or implementation support
- Guaranteed response times
- Commercial support or SLAs

---

## Opening Issues

Issues are welcome for:

- Specification ambiguities or contradictions
- Documentation errors or omissions
- Conformance fixture problems
- Suggestions for clarification (not scope expansion)

When opening an issue:

1. Search existing issues first
2. Provide specific references to affected documents
3. Include concrete examples where applicable
4. Avoid scope expansion requests in bug reports

---

## Contribution Expectations

This project follows a **conservative change policy**.

Contributions are evaluated on:

- **Clarity:** Does this reduce ambiguity?
- **Stability:** Does this maintain backward compatibility?
- **Scope:** Does this stay within v0.1 boundaries?
- **Testability:** Can this be verified with conformance fixtures?

Contributions that expand scope, add new guarantees, or change existing semantics will generally be declined for v0.1.x releases.

---

## Response Times

This is a volunteer-maintained project. Response times vary. Critical issues are prioritized, but no guarantees are made.

---

## Related Documents

- [SECURITY.md](SECURITY.md) — Security issue reporting
- [GOVERNANCE.md](GOVERNANCE.md) — Project governance
- [RELEASE_CHECKLIST.md](RELEASE_CHECKLIST.md) — Release process
