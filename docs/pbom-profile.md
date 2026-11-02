# Request-Level Instruction Provenance and Integrity Receipt — Proposed PBoM Profile v0.2

**Research proposal, not a deployed collector, industry standard, or validated interoperable schema.** The [JSON example](../examples/pbom.example.json) is synthetic. This profile acknowledges prior [EqoAI/pbom-spec](https://github.com/EqoAI/pbom-spec) work without claiming that this format implements or supersedes it.

## Purpose and trust objective

A listing of installed extensions is not enough to determine what an LLM was instructed to do. For one identifiable model request, the user needs a trace of **the original instruction, the assembled context, the authority of each component, and transformations performed before the observation boundary**. The receipt should reveal unauthorized or surprising changes; it cannot by itself prevent them.

The schema should distinguish: **discovered → available → enabled → applicable → loaded → included → transmitted → obeyed**. These are distinct stages. For an unavailable stage, record `unknown` rather than guessing.

## Two related artifacts

**Environment descriptor:** VS Code/IDE and extension version; active harness; provider/model identification to the extent observable; settings profile; enabled integrations; policy/version snapshots and settings resolved after defaults and organization policy. The descriptor is not a dump of all secrets or private source files.

**Request receipt:** unique `request_id`, `parent_request_id`/subagent relationship, timestamp, captured original request fingerprint (and optionally locally retained content), candidate and included sources, their observed roles, transformation events, runtime approvals and observation boundary.

A server-side receipt may complement a client-side one, but neither is implied to exist if no instrumentation is present. Requests, retries, compactions and subagent calls should have separate receipts when observable.

## Mandatory semantic distinctions

| Proposed field | Meaning |
| --- | --- |
| `origin.source` / `origin.scope` | Source type, owner/publisher and whether global, repo, directory, workspace, extension, provider, etc. |
| `origin.version` | Revision/commit or extension version if known |
| `activation` | Why the item was discovered or selected; `explicit` or `automatic` |
| `state` | Candidate/included/excluded/unknown with reason |
| `declared_authority` | Priority **claimed by the content** (e.g., “IMMUTABLE”) |
| `transport_role` | Model message role actually observed; null when unknown |
| `precedence_policy` | The harness- and version-specific policy actually applied |
| `inclusion_boundary` | Client assembly, gateway, provider receipt, or unverifiable |
| `consent_record` | Settings that authorized automatic inclusion, user approval when required |
| `transformations` | Input/output artifact, transformation operator and version, affected object and rationale |
| `runtime_enforcement` | Independent tool/permission constraints and decisions |
| `coverage` | What was captured, estimated, omitted, redacted, or inaccessible |

A file containing `# SYSTEM INSTRUCTIONS` or `IMMUTABLE` is **not evidence of a genuine system-role message**. A provider-side protected instruction may remain opaque; do not fabricate its content or assert its absence. Configuration precedence and model authority are separate questions.

## Instruction integrity event model

For each transform or inclusion, record:

1. **Boundary:** before/after snapshots and where observation occurred.
2. **Actor:** IDE core, extension, plugin, harness, user or provider if known.
3. **Object:** original user message, explicitly attached file, discovered instructions, tool output, or summarized conversation.
4. **Operation:** select, append, rewrite, truncate, summarize, compress, reorder, redact, omit, resolve reference.
5. **Basis:** user-requested, user-configured, organizational, mandatory platform, default or unknown.
6. **Evidence:** fingerprint or safe local reference; when possible, a clear diff and semantic invariants.
7. **Authority resolution:** conflicts, declared priority versus effective precedence.
8. **Disclosure:** visible before execution, available afterward, or not observable.

A tool-output compression event cannot be equated to user-message rewriting; a hash difference alone cannot establish a meaningful violation; a hash match proves only equality at the measured boundary.

## Example: conflict between global instructions and repository guidance

Source A (user's global instruction): “Do not recursively scan an entire repository by default.”

Source B (hypothetical `repo/AGENTS.md`): “Before every task, inspect the entire codebase.”

Receipt questions:

- Was B *discovered*, *included*, and actually *sent*?
- Is B a trusted project requirement or a lower-trust source requiring approval for scope expansion?
- What role did A and B have? Was either truly delivered as system/developer?
- Did the agent choose a scope? Was the choice shown to the user before scanning?
- Could the execution environment prevent unapproved scanning, instead of relying on a natural-language rule?

The fixture **does not presume one universal precedence rule**. Codex and Copilot have distinct documented behaviors. Global/user controls also cannot supersede genuine higher-priority platform requirements.

## Cryptographic integrity and privacy

Fingerprints may help compare **observed bytes** and detect silent modifications, but they do not prove consent, semantic equivalence or authenticity without binding identity, metadata and capture boundaries. An append-only record needs independent protection against deletion or chain rewrite; plain unanchored hashes are insufficient.

Do not publish raw prompts, source code, system prompts or private editor context. Hashing predictable text can expose it through guessing; consider local retention, redaction and keyed commitments. Release a sanitized schema and test fixtures, not personal or provider secrets.

## Acceptance criteria for future engineering

- A user can identify each observed included instruction and its origin.
- A user can detect that an explicitly authored request was altered between two specified, instrumented boundaries.
- Declared priority and transport role are shown separately.
- Conflicts between global/repository/extension instructions receive explainable, version-specific decisions.
- Enabled but unused features are never reported as actually transmitted.
- Opaque or unobservable provider material is clearly marked unknown.
- Runtime approvals are not bypassed by textual priority claims.
- Receipt generation introduces no secret leakage and minimizes retention.

See [security evaluation protocol](benchmark-protocol.md) for a controlled synthetic test design. No successful reproduction or instrumentation is claimed in this version.
