# LOSSLESS — Definition and Scope

## Definition
Lossless in KDF means preservation of structure, semantics, and
provenance within explicitly defined and testable bounds.

## Structural Losslessness
Guaranteed:
- Hierarchical structure
- Ordering
- Parent–child relationships

Not guaranteed:
- Visual layout
- Pagination
- Formatting fidelity

## Semantic Losslessness
Guaranteed:
- No inference
- No paraphrasing beyond normalization
- Direct equivalence to source text

## Provenance Losslessness
Guaranteed:
- Every atom is traceable to source evidence
- Source versions are immutable

## Exclusions
Lossless does NOT mean:
- Byte-for-byte reconstruction
- Completeness
- Truth assessment

Lossless does NOT imply that all content from a source is captured.
Extraction scope is explicitly bounded and declared.

## Language Requirements
The word "lossless" MUST NOT be used without specifying the bounds
within which losslessness is claimed. Unqualified claims of losslessness
are non-compliant.

Compliant usage:
- "lossless with respect to structure, semantics, and provenance
   within explicitly defined bounds"

Non-compliant usage:
- "lossless extraction"
- "lossless representation"

## Compliance
Claims of losslessness MUST satisfy all conditions above.
