# Evidence Addressing

## Principle
Evidence is valid only relative to an immutable source version and
declared extraction pipeline.

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

Invalid evidence MUST NOT be used for reasoning.
