# Release Checklist

This document defines the release process for KDF specification versions.

---

## Pre-Release Checks

Before tagging a release:

- [ ] All normative documents are internally consistent
- [ ] CHANGELOG.md is updated with all changes
- [ ] Version numbers are updated in kdf-v0.1.md (if applicable)
- [ ] No dangling TODOs in normative documents
- [ ] Cross-references between documents are valid
- [ ] Conformance fixtures in `conformance/` are complete
- [ ] Reference validator passes all conformance fixtures

---

## Release Steps

1. **Final review:** Re-read all changed documents for clarity
2. **Update CHANGELOG.md:** Ensure date and version are correct
3. **Commit:** Create final commit with message format:
   ```
   Spec: release v0.1.x
   ```
4. **Tag:** Create annotated tag:
   ```bash
   git tag -a v0.1.x -m "KDF Specification v0.1.x"
   ```
5. **Push:** Push commits and tags:
   ```bash
   git push origin main
   git push origin v0.1.x
   ```
6. **GitHub Release:** Create release on GitHub with:
   - Tag: `v0.1.x`
   - Title: `KDF Specification v0.1.x`
   - Body: Copy relevant CHANGELOG section

---

## Post-Release

- [ ] Verify GitHub Release is visible
- [ ] Verify tag is accessible
- [ ] Notify kdf-validator maintainers if conformance fixtures changed
- [ ] Update any external documentation referencing the spec

---

## Stability Commitment

- Patch releases (0.1.x) MUST NOT change existing semantics
- Patch releases MAY add clarifications and documentation
- Patch releases MAY add conformance fixtures
- Breaking changes require a minor or major version bump

---

## Rollback

If a release contains errors:

1. Do NOT delete tags
2. Do NOT force-push
3. Create a new patch release with corrections
4. Document the error in CHANGELOG.md

---

## Related Documents

- [CHANGELOG.md](CHANGELOG.md) — Version history
- [GOVERNANCE.md](GOVERNANCE.md) — Project governance
- [SUPPORT.md](SUPPORT.md) — Contribution expectations
