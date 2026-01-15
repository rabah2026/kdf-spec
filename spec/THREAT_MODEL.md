# Threat Model

This document defines the security model for KDF artifacts.
It establishes what KDF protects against, and critically, what it does not.

## 1. Assets

The primary assets protected by KDF are:
- **Evidence Integrity**: Assurance that a claimed fact is supported by a specific source span.
- **Provenance**: The ability to trace every piece of knowledge back to its origin.
- **Auditability**: The capability to machine-verify the link between content and source.
- **Stability**: Assurance that the underlying source has not changed since extraction.

## 2. Adversaries & Threats

KDF protects against the following threat actors and scenarios:

- **The Hallucinating Extractor**: An AI model that invents facts not present in the source.
- **The Stale Document**: A source file that has been updated or modified after data extraction.
- **The Lazy Human**: An editor who manually alters content without updating the backing evidence.
- **The Broken Chain**: A reference to a node or paragraph that no longer exists or has moved.

## 3. Security Guarantees

KDF provides the following BOUNDED guarantees when validated with a compliant validator:

### 3.1. Drift Prevention
If the source document changes (even by one byte), the `source_hash` check MUST fail.
This guarantees that evidence is never evaluated against a different version of the text than specifically intended.

### 3.2. Anti-Forgery (Fingerprints)
If `validation.status` is "valid", the `span_fingerprint` MUST match the text at the specified location.
This prevents "silent drift" where coordinates point to valid text that says something different than expected.

### 3.3. Path Integrity
All `node_path` references are validated as complete chains.
This prevents pointing to a non-existent hierarchy (e.g., a real paragraph ID nested under a fake section ID).

## 4. Non-Guarantees (Out of Scope)

KDF does **NOT** guarantee:

- **Truth**: KDF ensures the source *says* X. It does not ensure X is true.
- **Completeness**: KDF does not ensure all facts from the source are captured.
- **Benevolence**: KDF cannot detect if the source document itself is malicious or contains harmful instructions.
- **Contradiction-Freedom**: KDF allows conflicting atoms if they are faithfully extracted.

## 5. Operational Requirements

To maintain these guarantees, operators MUST:

1.  **Store Source Hash**: Every evidence entry MUST include the SHA-256 hash of the source version used.
2.  **Record Pipeline Identity**: The specific software/model version used for extraction SHOULD be recorded.
3.  **Invalidate on Mismatch**: If a validator reports a hash or fingerprint mismatch, the evidence MUST be treated as invalid immediately.
