# Changelog

All notable changes to the KDF specification are documented in this file.

## [0.1.1] - 2026-01-15

### Added
- TERMS.md: Normative definitions for knowledge, atom, evidence, and
  validation status meanings (valid/needs_review/invalid).

### Changed
- LOSSLESS.md: Added explicit language requirement that "lossless" MUST NOT
  be used without bounds qualifier. Clarified that lossless does NOT imply
  completeness.
- EVIDENCE_ADDRESSING.md: Strengthened requirement that evidence MUST be
  tied to an immutable source version (sha256). Added explicit failure mode:
  mismatched source hash MUST NOT have status "valid".
- CONFORMANCE.md: Added Non-Goals section explicitly excluding contradiction
  detection and resolution from v0.1 scope.
- kdf-v0.1.md: Added TERMS.md to list of normative documents.

## [0.1.0] - 2026-01-15

### Added
- Initial KDF v0.1 specification
- LOSSLESS.md: Definition and scope of losslessness
- EVIDENCE_ADDRESSING.md: Evidence reference requirements
- CONFORMANCE.md: Conformance suite requirements
- STYLE_GUIDE.md: Terminology and language rules
- Governance, licensing, and attribution documents
