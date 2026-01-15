# Source Canonicalization

To ensure reproducible `source_hash` and `span_fingerprint` verification, KDF requires strict source canonicalization. This document defines the REQUIRED procedures for different media types.

## 1. The Source Hash Principle

The `source.sha256` field MUST match the SHA-256 digest of the **canonicalized** source content. It MUST NOT be calculated on raw file bytes unless the raw file is already in canonical form.

## 2. Plain Text (text/plain)

For plain text documents, the following canonicalization pipeline MUST be applied before hashing:

1.  **Decode**: Decode bytes using UTF-8. Error handling MUST be distinct (fail or replace), but UTF-8 is the required standard.
2.  **BOM Stripping**: If a Byte Order Mark (BOM) `\ufeff` is present at the start, it MUST be removed.
3.  **Line Ending Normalization**: All line breaks (CR `\r`, CRLF `\r\n`) MUST be normalized to a simple Line Feed (LF `\n`).
4.  **No Trimming**: Trailing whitespace at the end of the file MUST be preserved unless explicitly defined otherwise by a specific pipeline.

**Formula**: `SHA256(UTF8_ENCODE(NORMALIZE_NEWLINES(STRIP_BOM(RAW_BYTES))))`

## 3. HTML (text/html)

HTML sources are volatile. To fingerprint an HTML source:

1.  **Extract Text**: Use a DOM text serialization method (e.g., `innerText` or equivalent).
2.  **Normalize**: Apply the Plain Text normalization rules (Section 2) to the extracted result.
3.  **Pipeline ID**: The extraction pipeline ID MUST be recorded in the evidence path, as different browsers/parsers may yield slight text differences.

## 4. PDF (application/pdf)

PDFs lack a standard text stream.

1.  **Extraction**: Use a consistent extraction library (e.g., pdfplumber, pypdf).
2.  **Pipeline Identity**: The specific library and version used MUST be recorded in `evidence.pipeline`.
3.  **Hashing**: The hash SHOULD be of the extracted text layer, not the raw PDF bytes, to allow for metadata updates (like signing) without breaking content validity.
    *   *Alternative*: Raw byte hashing is permitted if bit-for-bit file integrity is the priority over content integrity.

## 5. Pipeline Identity

Evidence SHOULD include a `pipeline` field identifying the software used to interpret the source.

Example: `pipeline: "kdf-text-extractor:v1.0.0"`
