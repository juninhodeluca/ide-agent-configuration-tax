# Legacy Data Templates — Historical v0.1 Productivity Study

**These CSV templates are archival and contain headers only. They are not evidence and are not the primary data design for v0.2.**

The initial paper proposed a developer productivity break-even study. Following the author's explicit correction, the main question is now **instruction integrity and provenance at the IDE–LLM boundary**. Keep these original templates only to preserve a transparent evolution of the project and avoid silently relabeling historic file formats.

- [runs-template.csv](runs-template.csv): historic task-level timing, quality and attention fields.
- [requests-template.csv](requests-template.csv): historic per-request usage and accounting fields.

Neither file includes measurements. Token volume anecdotes were not audited and are irrelevant to the revised paper's main argument.

## Primary v0.2 measurement candidates

A future instrument should record only appropriately sanitized data:

| Group | Proposed fields |
| --- | --- |
| Capture | request ID, session ID, client/harness/version, capture boundary |
| User request integrity | locally protected original fingerprint, comparison fingerprint, transformation disclosed |
| Source provenance | instruction ID, origin/publisher, version, scope, activation reason |
| Application | candidate, enabled, eligible, loaded, transmitted, not observed, unknown |
| Authority | declared priority, observed transport role, actual conflict rule |
| Transformations | operator/version, input/output IDs, affected object, semantic invariants |
| Consent | automatic versus explicit attachment, applicable user/organization setting |
| Runtime enforcement | action, required approval, decision, effect |
| Outcomes | source attribution accuracy, conflict resolution, anomaly detection, false positive classification |

A security-focused CSV or JSON schema should be frozen only after the capture boundary and privacy policy are agreed. **Unknown is not zero**. Do not expose confidential prompts, private source files, system text or raw identities for reproducibility. See the [revised evaluation protocol](../docs/benchmark-protocol.md) and [PBoM profile](../docs/pbom-profile.md).
