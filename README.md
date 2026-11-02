# When Defensive Agent Instructions Became a Source of Uncertainty

**A first-person account of global prompts, unexpected instruction sources, and a concern about alignment.**

**Juninho De Luca · English · Version 0.3.0 (November 2, 2026)**

I wrote global instructions for my AI coding assistant using the term **`IMMUTABLE`**. I was trying to prevent other instruction sources—repository files, skills, plugins, extensions, automatic context and agent harnesses—from unexpectedly overriding my operating preferences or changing the meaning of my requests.

After reading OpenAI's article about frontier-model misalignment, I wondered whether my defensive language might itself look like an attempt to subvert the instruction hierarchy. **Had I tried to protect the user-to-model communication in a way that appeared to violate the alignment rules I wanted to respect?**

This repository documents that question, how it arose, and the evidence available to me. I do not allege that a provider altered my prompts, that an injection occurred, or that a monitoring system classified my behavior as malicious.

## Read the account and accompanying material

- **[First-person case report (English)](paper.md)** — full narrative: the context, why I wrote the rules, what the misalignment publication made me question, and what remains uncertain.
- **[Appendix A — My complete global Codex instructions](case-studies/defensive-global-instructions.md)** — original English text, reproduced verbatim as the primary case artifact.
- **[Evidence catalog and screenshots](evidence/README.md)** — nine VS Code settings captures and one Codex Web personalization capture, with explicit limits of interpretation.
- **[References](references.md)** — the OpenAI misalignment article, Codex instruction-loading guidance, and relevant vendor documentation.
- **[Project history](ROADMAP.md)** — how this report evolved from earlier, broader technical drafts.

## The question

> When I send a request through an AI agent, how can I understand whether the instructions it ultimately received still represent what I intended and authorized?

The IDE was the setting in which I first noticed the issue, but the same uncertainty can arise in other **applications, plugins, extensions, skills, and harnesses** that contribute instructions or context.

I am sharing an account, **not proposing a solution**. The goal is to invite discussion with AI alignment, safety, and agent-engineering researchers and allow them to use their own analytical methods.

## Evidence and uncertainty

The screenshots document visible settings; they do not prove that any particular transformation was applied to my request. The global instructions establish the wording and purpose I intended; they do not prove the message role assigned by the harness. I have no evidence that my instructions were flagged as `scheming` or `prompt injection`.

## Scope of this revision

Version 0.3 removes the previous proposed **Prompt Bill of Materials**, benchmark, and testing framework from the active branch. They are not part of this invitation and remain accessible only through Git history. This version preserves the underlying screenshots and original case text.

**Author:** Juninho De Luca. AI-assisted writing, human editorial responsibility. This is a personal case report and invitation, not a vulnerability disclosure, peer-reviewed result, or official position of OpenAI or Microsoft. No new external issues or invitations have been sent from this repository.
