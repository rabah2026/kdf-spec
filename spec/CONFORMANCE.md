# KDF Conformance Suite v0.1

## Purpose
Defines objective compliance for KDF artifacts and validators.

## Rule
An implementation is KDF-compliant if and only if:
- All valid fixtures pass
- All invalid fixtures fail
- Edge cases are classified correctly

## Scope
Conformance applies to:
- KDF documents
- Validators

It does NOT apply to:
- Extraction pipelines
- AI models
- Reasoning systems

## Non-Goals
The following are explicitly out of scope for KDF v0.1:
- Contradiction detection
- Contradiction resolution
- Truthfulness evaluation
- Inference or reasoning

KDF artifacts MAY contain conflicting atoms if both are evidence-grounded.
The presence of contradictory statements from different sources (or the same
source) does not constitute a conformance failure.

## No Partial Compliance
Partial compliance is not compliance.
