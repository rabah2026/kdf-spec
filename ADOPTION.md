# KDF Adoption Guide

This document describes how KDF fits into real systems and what operators should expect.

---

## Where KDF Fits

KDF is an **evidence and provenance layer**. It sits between:

- **Upstream:** Source documents (text files, normalized HTML, extracted PDF text)
- **Downstream:** Applications consuming structured knowledge (search, Q&A, compliance tools)

KDF artifacts capture:

1. What knowledge was extracted
2. Where it came from (source + location)
3. How it can be verified (fingerprints, hashes)

KDF does NOT replace extraction pipelines, storage systems, or application logic.

---

## What KDF Is NOT

| KDF is NOT | Explanation |
|------------|-------------|
| An extraction engine | KDF validates artifacts; it does not create them |
| A knowledge base | KDF artifacts are portable records, not a database |
| A quality metric | Valid KDF says nothing about extraction quality |
| A completeness guarantee | KDF does not claim all knowledge was captured |
| A contradiction detector | KDF does not identify conflicting claims |
| An AI quality score | KDF makes no claims about LLM or RAG behavior |

---

## Recommended Operating Model

### Source Storage

- Store source documents in a content-addressable or versioned system
- Compute and preserve SHA-256 hashes at ingestion time
- Do not modify sources after hash computation

### Extraction

- Use deterministic extraction pipelines where possible
- Record `pipeline_id` in artifact metadata
- Compute `span_fingerprint` for all evidence with status `valid`

### Validation in CI

- Run `kdf validate` on all artifacts before deployment
- Run `kdf conformance` against the official fixture suite
- Fail builds on validation errors

### Artifact Storage

- Store KDF artifacts alongside or linked to source documents
- Preserve artifacts for audit trail purposes
- Consider artifact versioning if extraction pipelines evolve

---

## Compliance Posture

### What Auditors Can Verify

- **Structural conformance:** Artifact matches KDF schema
- **Hash integrity:** Source hash matches stored source
- **Fingerprint anchoring:** Evidence spans are verifiable
- **Pipeline identity:** Extraction process is documented

### What Requires Governance

- **Extraction quality:** Auditors cannot verify extraction correctness from KDF alone
- **Source authenticity:** KDF trusts the source hash; source provenance is external
- **Contradiction resolution:** KDF does not resolve conflicting atoms
- **Completeness claims:** Governance must define completeness expectations separately

---

## Change Management When Sources Drift

Sources may change over time. When this happens:

1. **Hash mismatch:** Validation will fail if source SHA-256 no longer matches
2. **Re-extraction required:** New artifacts must be generated from updated sources
3. **Artifact versioning:** Preserve old artifacts for historical audit
4. **No silent updates:** Do not modify artifacts without re-validation

KDF enforces immutability at the source level. Operators must manage source lifecycle externally.

---

## Integration Checklist

Before deploying KDF in production:

- [ ] Source storage preserves SHA-256 hashes
- [ ] Extraction pipeline records `pipeline_id`
- [ ] All `valid` evidence includes `span_fingerprint`
- [ ] CI runs `kdf validate` on all artifacts
- [ ] Artifact storage is durable and versioned
- [ ] Governance defines what "completeness" means for your domain
- [ ] Change management process handles source updates

---

## Related Documents

- [QUICKSTART.md](QUICKSTART.md) — End-to-end example
- [THREAT_MODEL.md](spec/THREAT_MODEL.md) — Security guarantees and non-guarantees
- [CONFORMANCE.md](spec/CONFORMANCE.md) — Conformance suite requirements
