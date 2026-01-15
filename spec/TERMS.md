# Normative Definitions

This document defines terms used throughout the KDF specification.
All terms defined here are normative and MUST be interpreted as specified.

## Terms

### Knowledge

Knowledge in KDF refers exclusively to explicit statements extracted directly
from authoritative source documents. Knowledge does NOT include:
- Inferred statements
- Paraphrased content beyond normalization
- Synthesized or derived conclusions

A statement qualifies as knowledge only if it can be traced to a specific,
inspectable location in a source document.

### Knowledge Atom

A knowledge atom is the smallest indivisible unit of explicit, evidence-backed
content in KDF. Each atom:
- MUST contain a payload representing the explicit content
- MUST be linked to at least one evidence entry
- MUST NOT contain inferred or synthesized information

Atoms are not evaluated for truthfulness; they record what a source states.

### Evidence

Evidence is a verifiable link between an atom and a specific span within a
source document. Each evidence entry:
- MUST reference a source by its immutable identifier (sha256 hash)
- MUST specify locators identifying the precise span
- MUST include a validation status

Evidence is valid only relative to a specific source version.

### Validation Status

The `validation.status` field indicates the operational state of an evidence
entry. The following values are defined:

| Status         | Meaning |
|----------------|---------|
| `valid`        | The evidence has been verified against the source. The span locators resolve correctly, and any fingerprints match. |
| `needs_review` | The evidence cannot be fully verified. This MAY occur due to source drift, fingerprint mismatch, or incomplete validation. Manual review is required. |
| `invalid`      | The evidence is known to be incorrect. The referenced span does not exist, the source hash has changed, or verification has explicitly failed. |

Evidence with status `invalid` MUST NOT be used for reasoning or downstream
processing without explicit acknowledgment of its invalidity.
