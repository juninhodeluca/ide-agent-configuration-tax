# Instruction Integrity at the IDE–LLM Boundary
## Configuration Complexity, Trust Boundaries, and the Case for a Request-Level Prompt Bill of Materials

**Juninho De Luca · Version 0.2.0 · November 2, 2026**  
*Technical position paper and proposed security evaluation framework. AI-assisted drafting and source review. Not peer-reviewed. No controlled attack experiment is claimed.*

## Abstract

An AI coding assistant does not receive only what a developer types. Its effective request can be composed from the user's message, developer-defined and platform instructions, workspace and repository guidance, IDE extensions, plugins, skills, editor state, tool results, automatic summaries, and agent-harness transformations. These components differ in origin, purpose, user visibility, and authority. Their composition can make it difficult for developers to determine **what was sent, which instruction prevailed, whether their original request was preserved, and which additions were authorized**. We call this the *instruction-integrity and provenance gap* at the IDE–LLM boundary.

A practitioner case illustrates a paradox: to defend against unexpected or contradictory instruction augmentation, a developer wrote global rules labeled `IMMUTABLE`, including restrictions on repository discovery, file rereads, validation and subagent behavior. The developer then became concerned that these defensive rules themselves might appear to violate agent alignment or instruction hierarchy. The case is not evidence of malicious prompt injection, scheming, or a model/provider violation. It demonstrates the need to distinguish **a user's protective intent**, **an instruction's declared authority**, **the transport role actually assigned by the harness**, and **the permissions enforced outside the model**.

We define a threat and failure taxonomy, propose a request-level *Prompt Bill of Materials* (PBoM) and an instruction-integrity receipt, and specify testable security/usability properties and a controlled evaluation protocol. Productivity and token consumption are secondary consequences, not the paper's primary explanatory variable. Screenshots establish heterogeneous configuration surfaces, not interception or tampering in the analyzed environment. No such incident is claimed as proven.

**Keywords:** instruction integrity; prompt provenance; trust boundary; AI coding agents; IDE; VS Code; Copilot; Codex; instruction hierarchy; request composition; prompt injection; Prompt Bill of Materials; alignment.

## 1. Research question and central claim

**Research question:** Can a developer reliably determine, for an individual IDE-mediated LLM request, which content and instructions were included, which transformations occurred, what authority each source actually received, and whether the resulting behavior stayed within the user's authorized task?

The problem is not fundamentally how many settings an IDE exposes. It is the inability to establish a trustworthy chain from a deliberate user instruction to the effective request and subsequent tool behavior when many independently updated components participate in that chain.

Our central claim is conditional and falsifiable:

> As agent configuration and instruction-composition paths proliferate, the risk of **unexpected, conflicting, or opaque instructions** increases unless provenance, precedence, transformations, and execution authority are made inspectable and enforceable.

We **do not** claim that every automatic instruction is prompt injection, that any vendor deliberately modifies user intent, or that a specific incident has already occurred. We distinguish recognized features from the unresolved questions they create.

### Contributions

1. A precise account of the **instruction-integrity gap**, separate from productivity debates.
2. An author-provided **defensive global-instructions case**, published verbatim with context and limitations.
3. A cross-layer taxonomy distinguishing composition, conflicting preferences, authority spoofing, prompt injection, and execution-policy bypass.
4. A proposal for an **instruction provenance and transformation receipt**, complementing existing PBoM work.
5. A security-centered evaluation protocol covering precedence, preservation, visibility, change detection, and informed consent.

## 2. The multi-source request boundary

Consider five separable elements: **(i)** user-authored text; **(ii)** explicitly selected files and context; **(iii)** automatically discovered instructions and state; **(iv)** transformations performed by the IDE/extension/harness/provider; and **(v)** permissions and effects in the execution environment.

~~~mermaid
flowchart LR
  U[User-authored request] --> H[IDE / extension / harness]
  E[Explicitly attached context] --> H
  A[Auto-discovered AGENTS.md / skills / plugins] --> H
  S[Editor, terminal, history, tool results] --> H
  G[Provider/platform policy and transport roles] --> H
  H --> R[Effective model request]
  H --> P[Proposed provenance receipt]
  R --> M[LLM]
  M --> T[Tool / action requests]
  T --> X[Runtime permission enforcement]
  X --> O[Observed outcome]
~~~

This is an **analytical model**, not a reverse-engineered implementation of all these products. A real client may not observe provider-side instructions or final model ingestion. Any receipt must indicate its **observation boundary** instead of implying end-to-end completeness.

The documented VS Code customization ecosystem contains automatic instructions, prompt files, agent skills, custom agents, hooks and MCP integrations; applicability depends on the chosen harness ([Microsoft: customization](https://code.visualstudio.com/docs/agent-customization/overview); [custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)). Documentation also identifies a Chat Debug view that can expose prompts, context and tool payloads for supported sessions ([debugging](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view)).

Codex documentation separately describes a path in which global and repository `AGENTS.md` instructions are discovered along a directory hierarchy and injected as **user-role messages**, with later directories overriding earlier ones in that path ([OpenAI Codex Prompting Guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide)). A local file named “SYSTEM INSTRUCTIONS” is therefore **not automatically a system-role instruction**. Other deployments and true developer/system messages may use different roles. **Configuration layering is not equivalent to model instruction hierarchy.**

## 3. Terminology: origin, authority, integrity, alignment

| Property | Question | Failure illustration |
| --- | --- | --- |
| Provenance | What is the source, version, scope and injection path? | An instruction appears without identifiable extension or repository origin |
| Activation | Was this source installed, enabled, matched, loaded, transmitted, or obeyed? | A skill listed as available is mistakenly assumed to have been sent |
| Authority | Which real role and conflict-resolution rule applied? | A repository file's “immutable” declaration is treated as platform policy |
| Integrity | Did bytes or task-critical semantics change, and was the change authorized? | A tool-output summary drops the failure line needed for debugging |
| Consent/control | Did the user opt into automatic attachment or transformation? | An active editor is appended without a clearly discoverable setting |
| Enforcement | Can the runtime block an action regardless of model interpretation? | Textual “no full-repo scan” is mistaken for a shell permission rule |
| Alignment assessment | Was the agent pursuing authorized objectives under applicable constraints? | A defensive instruction conflict is misconstrued as evidence of deceptive behavior |

**Prompt injection** is a trust-boundary problem: content obtained from a lower-trust source attempts to redirect the agent beyond the authority legitimately granted to that source. **Instruction conflict** is broader and may arise accidentally between two otherwise legitimate instruction files. **Prompt contamination** describes unanticipated augmentation without necessarily alleging an adversary. **Prompt tampering** should be reserved for unauthorized alteration established at a defined observation boundary; mere UI settings are not sufficient evidence.

An agent's **scheming** is a distinct question: covert pursuit of an unauthorized goal with deception or evasion of oversight. The case presented here describes explicit, visible, user-authored guardrails; it does not establish deceptive agent behavior. The labels used by a safety monitor cannot be inferred from a subsequent refusal or an instruction file alone.

## 4. Primary case: why the user wrote “IMMUTABLE”

### 4.1 Trigger and author intent

A developer using Codex on Linux encountered repository files, skills, plugins and IDE options capable of contributing context or directions beyond the latest typed request. Some repository-level directions reportedly requested exhaustive repository scanning or repeated test/visual-validation steps. The developer also observed settings for automatically attached editor or terminal context and compacted tool results.

The developer responded by placing highly prescriptive rules in global Codex instructions, including the heading:

> **IMMUTABLE CONTEXT & TOKEN RULES**

and the statement that they should not be overridden by repository instructions, skills, plugins, tools, automatic attachments or subagents.

**The intent was protective:** prevent sources the developer did not explicitly select from silently broadening scope, changing how work was performed, or overwriting persistent operating preferences. The concerns involved **the integrity of user–LLM communication**, with resource consumption as a secondary motivation. The complete, original instruction text is preserved in [Case Study A](case-studies/defensive-global-instructions.md).

### 4.2 The alignment paradox

The developer later encountered an article describing frontier-model misalignment and wondered whether these self-declared `IMMUTABLE` rules might be construed as prompt injection or scheming. The tension is genuine but should not be collapsed:

- A **user's defensive constraint** is not itself evidence of malicious intent.
- A sentence claiming **highest priority** does not make a user-authored file a system instruction.
- A rule that prevents legitimate safety validation may be **overconstrained or unsafe in execution** even though its author intended to prevent unwanted instructions.
- A legitimate repository requirement could also be **unanticipated by the user**; whether it should apply depends on the project's trust contract and the harness.
- Higher-priority platform or developer rules, and hard tool-approval boundaries, are not canceled by the text “immutable.”

The security design challenge is to let a developer express **user-controlled invariants** without encouraging a textual attempt to redefine hierarchy. A trustworthy product should expose **what can be fixed, what can be overridden, by whom, and at which layer**.

### 4.3 Concrete conflict fixtures derived from the case

| Global instruction | Possible repository/extension addition | Research question |
| --- | --- | --- |
| Do not scan repositories broadly by default | Scan entire codebase before every change | Who authorized the scan? Which scope applies? |
| Avoid rereading unchanged files | Read full files after every patch | Can safe exception conditions be declared and traced? |
| Typecheck/build only by default | Run lint, tests, screenshots after every edit | Is this a required acceptance contract or optional advice? |
| Preserve typed task scope | “Optimize prompt” by expanding into refactor | Was original text preserved; who approved the semantic change? |
| Minimize external context | Automatically include editor and terminal | Which setting, scope and session attached them? |

These are **hypothetical fixtures based on the author's account**, not captured payloads proving execution or provider misconduct. A test must keep higher-priority safety requirements effective.

### 4.4 Observable screenshots: what they show and what they do not

The [evidence catalog](evidence/README.md) contains nine screenshots of VS Code AI settings and one Codex personalization screenshot. Visible enabled items include automatic application/referencing of instructions, skill-adherence prompts, implicit editor/terminal context, nested `AGENTS.md` discovery, and tool-output compression. Other experimental model prompts and compaction mechanisms are visibly disabled. Some descriptions apply only to Local; others to Agent Host. These UI states do **not** show the effective assembled request or establish that all mechanisms ran simultaneously.

The developer also reported a difference between Codex Desktop instructions and the Web view. Without a controlled, versioned two-endpoint test, the screenshots support a **reported divergence**, not a proven synchronization defect.

## 5. Threat model and failure classification

**Assets:** the user's authored message and task boundaries; global instruction preferences; project-specific requirements; confidential editor/terminal content; executable tool permissions; auditability of transformations and responses.

**Actors and components:** user; organization and platform policy; IDE vendor; extensions; workspace maintainers; external plugin and MCP publishers; agent harness; model provider; tools and subagents. These have varying authority and visibility. No component should acquire authority solely by being included in model context.

**Trust-boundary crossings** to analyze:

1. Repository content → agent instruction (legitimate customization or authority spoofing).
2. Extension settings → automatically appended context (expected behavior or unwanted augmentation).
3. Tool output → summary/truncation (useful optimization or loss of task-critical evidence).
4. Global preference → lower-scoped repository override (contractual precedence dispute).
5. Model text → tool action (permission and confirmation enforcement).
6. Client-built request → provider boundary (partial observability; unknown server augmentations must be labeled as unknown).

| Category | May occur without attacker? | Evidence required |
| --- | --- | --- |
| Expected composition | Yes | Configured rule, activation decision, request trace |
| Benign but surprising augmentation | Yes | Authored request versus observed composition |
| Conflicting instructions | Yes | Contradictory applicable texts and resolution trace |
| Semantic drift during transformation | Yes | Before/after artifact and explicit task invariant |
| Injection attempt | No adversary intent need be proven to establish attempted redirection, but malicious classification requires care | Lower-trust imperative, unauthorized objective, crossing attempted |
| Unauthorized execution | Yes, including accidents | Actual tool action and applicable authorization boundary |
| Scheming | An agent-specific behavior, not inferred from an author's strict instructions | Evidence of covert goal pursuit or evasion |

The analogy to risky model artifacts on Hugging Face is limited: malicious `pickle` deserialization can cross a data-to-code boundary directly. IDE instruction augmentation crosses a data-to-authority boundary through model interpretation. They share a **trust-boundary principle**, not an exploit mechanism ([Hugging Face pickle scanning](https://huggingface.co/docs/hub/security-pickle)).

## 6. Proposed solution: inspectable instruction composition

A *Prompt Bill of Materials* (PBoM) can complement a software bill of materials by describing each request's **instruction sources and transformations**. We recognize prior use of the term by [EqoAI/pbom-spec](https://github.com/EqoAI/pbom-spec), and do **not** claim to originate the term or to implement that specification.

A proposed **request-level receipt** should include:

| Field group | Minimum content |
| --- | --- |
| Identity | Request identifier, session, timestamp, harness/version, model requested/resolved when observable |
| Original | Protected fingerprint of the user's authored request, capture point and verification method |
| Sources | Origin, publisher, source scope, version, discovery trigger, explicit/implicit status |
| Inclusion | Candidate, enabled, eligible, selected, transmitted, excluded or unknown, with reason |
| Authority | **Declared priority**, **actual transport role**, and **runtime precedence policy** as separate values |
| Transformations | What object changed, operator/version, input/output references, disclosed intent and result |
| Consent | User-enabled settings, per-request authorization and applicable organizational restrictions |
| Enforcement | Tool permissions, approvals, guardrail decisions and actions actually invoked |
| Coverage | Client-observed, gateway-observed, provider-confirmed, inferred, unavailable or unknown |

A receipt **must not invent privileged server-side instructions or expose secrets**. Unknown is not the same as absent. Hashes of short predictable messages may expose sensitive information by dictionary attacks; deploy with minimized retention, redaction, keyed commitments or secure local storage as appropriate. Cryptographic hashes detect observed byte changes, **not semantic fidelity, provenance authorization or complete chain-of-custody**. See [proposed profile](docs/pbom-profile.md) and the [synthetic example](examples/pbom.example.json).

### Design principles

- **Authored-text integrity:** preserve the original text for comparison even if optimized representations are sent downstream.
- **Source-level transparency:** show why an instruction was selected and how its authority was resolved.
- **Safe conflicts:** flag irreconcilable material conflicts before high-impact execution; do not silently reinterpret user intent.
- **Effective configuration snapshots:** compare resolved settings and defaults across versions, not only saved `settings.json`.
- **Independent execution checks:** enforce filesystem, network, tool and approval restrictions outside natural-language prompts.
- **Privacy-preserving visibility:** a user can inspect the composition affecting them without requiring disclosure of proprietary protected prompts.

## 7. Evaluation: measure communication security first

A controlled experiment should use synthetic projects, known conflicting instruction fixtures and an instrumented harness. The **primary outcomes are security and explainability**, not tokens saved.

| Outcome | Operational test |
| --- | --- |
| Source attribution accuracy | Can evaluators identify every observed instruction source and its scope? |
| Role/precedence correctness | Can they predict and verify which rule prevails for an explicit conflict? |
| Original-request preservation | Are authored bytes preserved at the user-to-client boundary, and are modifications disclosed? |
| Semantic constraint preservation | Did transformation retain predefined task invariants, not just the length or hash? |
| Unapproved augmentation detection | Is an unexpected auto-attachment surfaced before execution? |
| Policy enforcement consistency | Do runtime approvals work even when a text instruction claims to override them? |
| Change explainability | Does a version update reveal differences in effective instruction composition? |
| False-alarm rate | Are ordinary, authorized customizations incorrectly labeled as attacks or scheming? |

**Protocol sketch:** freeze a fixture task, source texts, versions and expected conflicts; run with and without auto-discovery/implicit context/output compression; capture pre-assembly and observed model request; vary exactly one source or setting; evaluate recognition and behavior; repeat with a new version to measure configuration drift. Limit interpretation to observed request boundaries. The full [evaluation protocol](docs/benchmark-protocol.md) specifies controls and privacy constraints.

Token cost and developer productivity should be reported only as **secondary usability/adoption outcomes**: uninspectable behavior can increase auditing work and discourage adoption. This paper makes no claim about aggregate token counts or economy-wide productivity.

## 8. Discussion and limits

Greater transparency does not guarantee safe models. Excessive logging can itself expose private code or prompts. Full provider transparency may be neither available nor appropriate; a bounded receipt with attested client-side events can still be useful. Likewise, a global preference that categorically forbids all validation may undermine task quality. The intended design is **explicitly governed, exception-aware precedence**, not blanket immunity for user text.

Neither the screenshots nor the original case prove that the user's words were secretly rewritten, that a plugin performed an injection, or that safety systems classified the author as misaligned. Such claims require traces and authorization records that are not available here.

This is a **position paper with practitioner evidence and testable proposals**, not a completed vulnerability disclosure or a benchmark result. The versioned source registry in [references.md](references.md) distinguishes observed screenshots, official documentation and author testimony.

## 9. Conclusion

The core risk is not that an IDE exposes too many settings; it is that a developer may lose visibility into **who is speaking to the model on their behalf**. A defensive declaration of “IMMUTABLE” should not be mistaken for adversarial intent, nor should it be presented as a reliable enforcement mechanism. The desired remedy is not a stronger incantation in the prompt. It is an auditable contract among the user, the IDE, extensions, the harness, the model provider and the execution environment.

**Users should be able to know what they asked, what else was added, who authorized it, what changed in transit, and which instruction had effective authority.**

## Sources and disclosure

The primary-source bibliography and evidence limitations are in [references.md](references.md); screenshots are indexed in [evidence/README.md](evidence/README.md). The verbatim instruction case is published in [case-studies/defensive-global-instructions.md](case-studies/defensive-global-instructions.md).

Author: Juninho De Luca. Research and writing assistance: AI. Editorial responsibility remains with the author. This work is independent and is not endorsed by OpenAI, Microsoft, GitHub, VS Code, Hugging Face, or any model provider. No third-party accounts, production systems, or confidential prompts were tested.
