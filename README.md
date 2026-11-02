# Instruction Integrity at the IDE–LLM Boundary

**A technical position paper about instruction provenance, user intent, trust boundaries, and configuration-induced ambiguity in VS Code, Copilot, Codex, and other agentic IDE environments.**

Version **0.2.0** · November 2, 2026 · Juninho De Luca · English  
Position paper / proposed methodology; not peer-reviewed; **no claim of a proven attack, unauthorized prompt rewrite, or controlled empirical result**.

## The central problem

An IDE-mediated LLM request may contain instructions and context that the developer never typed: repository guidance, extensions, plugins, skills, editor and terminal context, tool outputs, and transformations by the harness. Even when each component is legitimate, the developer may lack visibility into **who supplied instructions, what authority they actually received, whether the original request was preserved, and what the agent was authorized to do**.

This is an **instruction-integrity and communication-security problem**, not primarily a token-efficiency or productivity problem.

> A developer should be able to determine what they asked, what else was added, which component added it, what changed in transit, and which instructions had effective authority.

## Read the research

- **[Full paper (English)](paper.md)** — thesis, threat model, terminology, defensive alignment paradox, PBoM proposal and testable security properties.
- **[Case Study A: Defensive Global Instructions](case-studies/defensive-global-instructions.md)** — the author's original global Codex Linux instructions, reproduced in full as an explicit example of protective `IMMUTABLE` rules.
- **[Request-level PBoM profile](docs/pbom-profile.md)** and **[synthetic JSON illustration](examples/pbom.example.json)** — a transparency and traceability proposal, not an implemented standard.
- **[Security-centered evaluation protocol](docs/benchmark-protocol.md)** — test conflicts, roles, transformations, source attribution and runtime enforcement using harmless fixtures.
- **[Screenshots and evidence limitations](evidence/README.md)** — nine VS Code settings screenshots and an additional Codex Web personalization screenshot.
- **[References and evidence ledger](references.md)** — original vendor documentation and scope of each claim.
- **[Research roadmap](ROADMAP.md)** — what has been published and what remains to be tested.

## Why the global-instructions example matters

The author encountered multiple mechanisms that could append instructions to IDE agent requests. In response, they wrote global rules labeled `IMMUTABLE` so that repository-level directions, plugins and skills would not silently override preferred scope, discovery or validation defaults. The same strict wording later raised a concern: could a defensive rule itself be interpreted as an instruction-hierarchy attack or an alignment violation?

The paper's answer is **conceptual, not diagnostic**:

- A user-authored defensive policy is not by itself *scheming* or *prompt injection*.
- A source can declare itself `IMMUTABLE` without acquiring actual system-role authority.
- Legitimate and unexpected instructions can conflict even without an attacker.
- Actual enforcement belongs in the harness/tool permissions, with explicit source and precedence visibility.

## What the evidence does and does not show

The screenshots show real configuration surfaces for automatic instruction inclusion, implicit context, model-specific prompts, skill adherence and output compaction. Some were enabled, others disabled, and some are harness-specific. They do **not** establish that the user's prompt was covertly rewritten, that every visible option affected a given request, or that an agent was flagged as misaligned.

No experimental capture has yet been run. The document separates observation, author report, vendor documentation, hypothesis and proposal. The prior v0.1 paper emphasized productivity break-even; **v0.2 corrects that emphasis**. Performance and adoption are secondary implications of lost trust and predictability. Anecdotal token volumes are not part of the argument.

## Intended audience and next steps

Security researchers, IDE/agent developers, human-computer interaction researchers, provider policy teams, and maintainers of extension or plugin systems. Next steps are to validate the provenance receipt and conduct instrumented, privacy-preserving tests across concrete harness versions. **Issues will not be opened in OpenAI or Microsoft/VS Code repositories until a separate discussion stage.**

This work builds on, but does not claim to originate, the phrase [Prompt Bill of Materials](https://github.com/EqoAI/pbom-spec); no compatibility with that project's schema is asserted.

## Authorship

Juninho De Luca. Research and drafting assisted by AI; final editorial responsibility belongs to the author. Not an official OpenAI, Microsoft, GitHub or VS Code publication. Screenshots and primary instruction artifact were supplied by the author. Use [CITATION.cff](CITATION.cff) to cite a specific version/commit. No reuse license has been selected.
