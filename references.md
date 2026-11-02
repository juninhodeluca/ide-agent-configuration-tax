# Source Register, Evidence Classes and Claim Boundaries

**Document revision: November 2, 2026.** Vendor documentation is mutable; pages linked here may change. The paper is a focused position analysis, not a systematic review or a verified vulnerability report.

## Primary documentation

| ID | Source | Supports | Does not establish |
| --- | --- | --- | --- |
| D01 | [VS Code — Customize agents](https://code.visualstudio.com/docs/agent-customization/overview) | Multiple customization forms, varying harnesses, relevance and scope | That every feature ran in the user's screenshot session |
| D02 | [VS Code — Custom instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions) | File discovery, `applyTo`, `AGENTS.md`, harness-specific behavior and conflict caveats | A universal role-precedence order |
| D03 | [VS Code — Debug chat interactions](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view) | Debug access to observed prompts, context and tools in supported sessions | Visibility into all provider-side assembly |
| D04 | [VS Code — Troubleshoot AI](https://code.visualstudio.com/docs/agents/agent-troubleshooting/troubleshooting) | Discovery diagnostics and interpretation of missing customizations | Proof of hidden tampering |
| D05 | [VS Code — Settings](https://code.visualstudio.com/docs/configure/settings) | User/workspace settings and effective configurations | Model instruction authority |
| D06 | [VS Code — Settings Sync](https://code.visualstudio.com/docs/configure/settings-sync) | Sync mechanisms within documented scope | Whether Codex Desktop and Web store identical objects |
| D07 | [OpenAI — Codex Prompting Guide (AGENTS.md)](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide) | Codex path with discovered AGENTS instructions as user-role messages and root-to-leaf ordering | All possible Codex deployments or that a title `SYSTEM` confers system authority |
| D08 | [OpenAI — Codex agent security](https://developers.openai.com/codex/security/) | Execution permissions and defense concepts (where supported) | That the analyzed case crossed any boundary |
| D09 | [OpenAI — Model Spec](https://model-spec.openai.com/2025-10-27) | General chain-of-command and untrusted data distinctions (versioned document) | How a specific IDE sent one message |
| D10 | [Model Context Protocol — Architecture 2025-06-18](https://modelcontextprotocol.io/specification/2025-06-18/architecture/index) | Host/client/server responsibilities and consent boundary | That all implementations respect those boundaries |
| D11 | [Hugging Face — Pickle scanning](https://huggingface.co/docs/hub/security-pickle) | Risk of executable deserialization in model artifacts | Prompt injection in IDEs, or this user's environment being compromised |
| D12 | [VS Code — Chat and diagnostics](https://code.visualstudio.com/docs/chat/chat-overview) | Debugging pathways and available configuration interfaces | Universal capture of all implicit content |

The Codex security URL may change; follow the official documentation navigation if relocated. D07 specifically describes **one** published instruction-transport path; avoid treating that as a universal OpenAI system-role mapping. D09 is cited as a versioned policy text, not proof of individual user or monitor classification.

## Prior work and conceptual analogies

| ID | Reference | Purpose and limits |
| --- | --- | --- |
| P01 | [NTIA — Minimum Elements for a Software Bill of Materials](https://www.ntia.gov/report/2021/minimum-elements-software-bill-materials-sbom) (2021) | Component/relationship analogy; not a specification for agent prompts |
| P02 | [EqoAI/pbom-spec](https://github.com/EqoAI/pbom-spec) | Prior usage of “Prompt Bill of Materials” and records of interactions/fingerprints; this repository claims neither first use nor schema compatibility |

The prior research draft included developer productivity studies (Peng et al.; METR) and anecdotal token figures. These are not evidence for the **instruction-integrity thesis** and are intentionally removed from the central argument. Productivity/adoption is a possible downstream implication only.

## Author-provided case evidence

| ID | Evidence | Warranted claim |
| --- | --- | --- |
| O01 | Nine VS Code settings screenshots, S01–S09 | Visible options and check states in one captured configuration, with mixed Local/Agent Host labels |
| O02 | One Codex Web personalization screenshot, S10 | Text in Web UI referring to synchronized Codex instructions |
| R01 | Author's account of global instruction conflicts with plugins/repository directions | Author motivation; not an independently verified injection incident |
| R02 | [Full defensive global instructions](case-studies/defensive-global-instructions.md) | An authentic example as supplied by the author for publication, not a representation of actual model transport or compliance |
| R03 | Reported Desktop/Web content mismatch | A claim that warrants a controlled cross-surface test, not a demonstrated bug |

All screenshot descriptions and limits are in [evidence/README.md](evidence/README.md) and fingerprints in [evidence/manifest.json](evidence/manifest.json). We do not publish unrelated chat text.

## Claims deliberately **not** made

- No evidence that the IDE or an extension covertly rewrote the developer's text in the reported session.
- No evidence that prompt-injection detection or scheming monitors flagged the author's instructions.
- No proof that all enabled toggles affected a single request; many are harness-specific.
- No verification of daily growth in option count.
- No claim that any specific vendor intentionally misled users, performed exfiltration or violated policy.
- No measured comparison of token volumes, developer productivity or economic break-even.

## Research integrity

Document explicit observations, distinguish UI enablement from actual inclusion, and record the boundary at which transport roles and transformations can be verified. When a provider or harness step is not observable, record `unknown`. The [evaluation protocol](docs/benchmark-protocol.md) proposes a way to generate evidence without guessing.
