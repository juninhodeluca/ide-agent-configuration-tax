# When Defensive Agent Instructions Became a Source of Uncertainty

**A first-person account of global agent instructions, the complexity of request assembly, alignment concerns, and individual responsibility when a request may change before reaching a model.**

**Juninho De Luca · English · Version 0.4.0 (November 2, 2026)**

I wrote global instructions for my AI coding assistant using the term **`IMMUTABLE`**. I was trying to protect my original requests and preferred execution boundaries against unexpected or conflicting instructions contributed by repository files, IDE extensions, skills, plugins, apps, and agent harnesses.

Reading OpenAI's publication on frontier-model misalignment made me wonder whether this defensive wording could itself be interpreted as an attempt to override instruction hierarchy.

As I reviewed my screenshots of agent settings, an additional concern became central: **the large, heterogeneous configuration surface can make it difficult to know what content actually reached the model**. Relevant information might have been omitted by a transformation; conflicting instructions might have been added from an auxiliary source. Either could affect the model's output. Those are **possibilities, not demonstrated events in my sessions**.

That uncertainty raises a question of responsibility:

> **If an intermediary materially alters a request before it reaches the model, how can responsibility for a resulting violation be fairly attributed to an individual user?**

This question is not a claim that users are automatically free from responsibility. It asks how user-authored instructions, user-authorized additions, application transformations, agent actions, and causal responsibility can be distinguished.

## Read the account and supporting materials

- **[First-person account (English)](paper.md)** — context, defensive `IMMUTABLE` wording, alignment uncertainty, output uncertainty and fair attribution of responsibility.
- **[Appendix A — Complete global agent instructions](case-studies/defensive-global-instructions.md)** — author's original English instruction text reproduced verbatim as a case artifact.
- **[Nine settings screenshots and evidence notes](evidence/README.md)** — shows the breadth of possible instruction/context composition and transformation controls, **not an instance of prompt injection**.
- **[References and evidentiary limits](references.md)** — relevant publications and a distinction between observed configuration and actual model requests.
- **[Editorial history](ROADMAP.md)** — evolution of the report and its scope.

## What the screenshots demonstrate—and what they do not

The nine images depict numerous controls potentially affecting instruction selection, context attachment, model-specific behavior and tool-output transformation. They document a complicated **configuration surface that may escape ordinary user attention**. They do not establish that any setting executed in a particular session, that an instruction was injected, that a prompt was covertly rewritten, or that relevant context was lost.

The original global instructions are included to explain the author's motivation and uncertainty, not to establish the existence of an exploit.

## Scope and invitation

The question is not specific to VS Code or Codex. Any app, plugin, extension, repository guidance, memory system or harness involved in preparing an LLM request may raise comparable questions about provenance and user authorization.

This report makes **no vulnerability allegation and no proposed test plan or engineering standard**. It invites researchers working on AI safety, alignment and human oversight to examine the situation through their own methods.

**Author:** Juninho De Luca. AI-assisted drafting; editorial responsibility remains human. Not a peer-reviewed study, a legal opinion, or an official OpenAI or Microsoft publication. No external research invitation has been sent as part of this revision.
