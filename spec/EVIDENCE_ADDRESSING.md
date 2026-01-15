# Evidence Addressing

## Principle
Evidence is valid only relative to an immutable source version and
declared extraction pipeline.

Evidence MUST be tied to an immutable source version, identified by
the source's sha256 hash. This binding is non-negotiable.

## Required Components
Each evidence reference MUST include:
- Source hash (sha256)
- Extraction pipeline identity
- Primary locator (offset or page/line)
- Anchor locator (fingerprint or node path)
- Validation status

## Locators
Primary locators provide precision.
Anchor locators provide stability.

Offsets alone are insufficient.

## Invalidation
Evidence MUST be invalidated if:
- Source hash changes
- Pipeline changes
- Fingerprints do not match

If the referenced source hash differs from the hash of the actual source
document, the evidence MUST be marked as `invalid` or `needs_review`.
Evidence with a mismatched source hash MUST NOT have status `valid`.

Invalid evidence MUST NOT be used for reasoning.
