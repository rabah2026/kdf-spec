# KDF Quickstart

This document provides a minimal, end-to-end example for creating and validating a KDF artifact.

**Time required:** ~5 minutes  
**Prerequisites:** Python 3.9+, `kdf-validator` installed

---

## Step 1: Prepare a Source File

Create a plain-text UTF-8 file. KDF requires deterministic source identification.

```
company_policy.txt
```

Contents:

```
All employees must complete security training annually.
Remote work requires VPN connection at all times.
```

Ensure the file is saved as UTF-8 without BOM.

---

## Step 2: Compute Source Hash

Use the `kdf hash-text` command to compute the canonical SHA-256 hash of the source:

```bash
kdf hash-text company_policy.txt
```

Output:

```
sha256:a1b2c3d4e5f6...  (64 hex characters)
```

This hash identifies the exact source version. If the file changes, the hash changes.

---

## Step 3: Compute Span Fingerprint

Extract a specific span and compute its fingerprint:

```bash
kdf fingerprint "All employees must complete security training annually."
```

Output:

```
sha256:7f8e9d0c1b2a...  (64 hex characters)
```

The fingerprint anchors extracted knowledge to the exact text span.

---

## Step 4: Create a Minimal KDF Artifact

Create a JSON file `policy_knowledge.kdf.json`:

```json
{
  "kdf_version": "0.1",
  "source": {
    "uri": "file:///path/to/company_policy.txt",
    "sha256": "a1b2c3d4e5f6..."
  },
  "document": {
    "id": "doc1",
    "type": "document",
    "children": [
      {
        "id": "p1",
        "type": "paragraph",
        "text": "All employees must complete security training annually."
      }
    ]
  },
  "atoms": [
    {
      "id": "atom1",
      "claim": "Employees must complete annual security training.",
      "evidence": [
        {
          "node_path": "document:doc1/paragraph:p1",
          "anchors": [
            {
              "type": "span_fingerprint",
              "algo": "sha256",
              "value": "7f8e9d0c1b2a..."
            }
          ],
          "validation": {
            "status": "valid"
          }
        }
      ]
    }
  ],
  "metadata": {
    "pipeline_id": "manual-extraction-v1",
    "extracted_at": "2026-01-16T12:00:00Z"
  }
}
```

Replace hash values with actual outputs from Steps 2 and 3.

---

## Step 5: Validate the Artifact

Run the validator:

```bash
kdf validate policy_knowledge.kdf.json
```

Expected output for a valid artifact:

```
PASS: policy_knowledge.kdf.json
```

If validation fails, the validator reports specific errors.

---

## Important Notes

### pipeline_id

The `pipeline_id` field identifies the extraction process that created the artifact. This is RECOMMENDED for traceability but does not imply any quality guarantee. Different pipelines may produce different knowledge from the same source.

### Valid Requires Fingerprint

Evidence with `validation.status` of `valid` MUST include at least one `span_fingerprint` anchor with `algo: sha256`. Evidence without a fingerprint cannot have status `valid`.

### What KDF Does NOT Provide

- **Completeness:** KDF does not claim all relevant knowledge was extracted.
- **Contradiction detection:** KDF does not identify conflicting atoms.
- **Semantic correctness:** KDF validates structure and provenance, not meaning.
- **Source quality:** A valid KDF artifact says nothing about source accuracy.

---

## Next Steps

- Read [TERMS.md](spec/TERMS.md) for normative definitions
- Read [ADOPTION.md](ADOPTION.md) for integration guidance
- Run `kdf conformance conformance/` to verify validator behavior
