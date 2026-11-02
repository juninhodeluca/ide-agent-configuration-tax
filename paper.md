# When Defensive Agent Instructions Became a Source of Uncertainty
## A first-person account of instruction uncertainty, alignment concerns, and responsibility for requests altered before reaching a model

**Juninho De Luca**  
**Case report and invitation to research discussion · Version 0.4.0 · November 2, 2026**  
*Written with AI assistance from the author's account and supplied artifacts. Not peer-reviewed. No allegation of a security incident or misconduct.*

## Abstract

I wrote unusually strict global instructions for my AI coding assistant because I wanted to prevent my original requests and working preferences from being silently displaced by repository files, skills, plugins, applications, IDE extensions, or other components of an agent harness. I called some of these instructions **“IMMUTABLE CONTEXT & TOKEN RULES.”** Later, OpenAI's publication on frontier-model misalignment made me wonder whether my defensive wording—intended to resist unexpected instructions—might itself be interpreted as an attempt to override an instruction hierarchy.

The uncertainty goes beyond my own configuration. The nine screenshots accompanying this account show a broad, heterogeneous settings surface capable, depending on the product, harness and active options, of influencing instruction selection, context inclusion, and transformations before a model receives an effective request. **The screenshots are not presented as evidence of prompt injection, an actual prompt rewrite, or a policy violation.** Their purpose is to illustrate why an ordinary user may find it difficult to know which instructions and information reached the model, what was omitted, and what was added.

This uncertainty matters both for confidence in outputs and for accountability. **If a request is materially altered before it reaches the model, on what basis can an individual user be held responsible for a resulting violation?** I do not claim that responsibility automatically disappears, or that this happened to me. I ask how platforms can fairly distinguish user-authored intent, changes knowingly authorized by the user, changes imposed by the application, and actions taken by an agent. This is a case report and an invitation to discussion, not a vulnerability disclosure, a technical proposal, or a claim of wrongdoing.

## 1. Why I began questioning the instructions reaching my assistant

I use AI assistants as part of ordinary software development. Over time, configuring an agent became less like choosing a model and more like managing an expanding collection of instruction sources: global and project files, skills, application integrations, IDE extensions, attached editor context, terminal output, memory, and model-specific settings.

I started examining files and settings under locations such as `~/.codex`, `~/.agents`, and `~/.copilot`, as well as project repositories. I repeatedly encountered guidance instructing agents to inspect large parts of the codebase, follow additional skills, perform repeated tests, validate visual output, or carry out discovery steps that I had not expressly requested for a given task.

Some of these instructions may have been legitimate and useful. Some belonged to different tools or execution environments. I did not have a reliable way to tell which ones were actually applicable to an individual request, which were merely installed or available, and which had been passed to the model.

What concerned me most was not the number of settings. It was the possibility that **I could write one request while the model received that request together with additional instructions that materially changed its scope or execution conditions**—and that I might not know exactly where those instructions originated.

The [nine settings screenshots](evidence/README.md) document the scale and diversity of the exposed configuration surface: automatic instruction inclusion, implicit context, skill-adherence prompts, nested `AGENTS.md` discovery, model-dependent options, and compression of tool results. Their role is **illustrative, not accusatory**. Enabled settings are not proof that any particular instruction was transmitted, while disabled settings are not evidence of an active effect. The difficulty is that a user may be unable to distinguish the product's *potential* behaviors from what happened during one concrete request.

## 2. The two situations that led me to write “IMMUTABLE”

### 2.1 Repository guidance overriding global preferences

I encountered repository-level instruction files that stated that local `AGENTS.md` guidance could supersede global instructions. I accept the basic idea that a project can define coding conventions, architectural restrictions, or tests necessary for its own correctness.

However, I did not want a repository file—possibly written long before I opened that project—to override **all** of my user-level operating preferences. For example, I wanted to avoid exhaustive codebase scans or repeated full-file reads when a narrower investigation was sufficient. Likewise, I did not want a default instruction to perform browser screenshots or comprehensive test suites after every small change unless the task or a real safety requirement justified it.

I therefore wrote a global section declaring certain context-management and execution rules “IMMUTABLE.” My intent was to establish a protected baseline against unexpected additions from lower-trust or less visible sources. I was **not** attempting to override platform safety policies, evade tool approvals, or grant myself authority over a model's protected system instructions.

Nevertheless, my wording made an absolute claim about precedence. Whether a particular client could actually honor that claim is a separate technical question.

### 2.2 Extensions and applications contributing instructions or transforming content

I also noticed settings and instruction files associated with IDE assistants and extensions that referred to operations such as optimizing prompts, compressing outputs, or automatically incorporating context. This disturbed me for a different reason.

I am not opposed to summarization, compacting tool results, or adding relevant context. I object to the **possibility of a material change in what I communicate to the assistant occurring without an intelligible record of the transformation or its source**.

I need to distinguish a concern from an observed event: I saw instruction text and configuration options describing these kinds of operations. I **did not capture before-and-after payloads proving that my own typed prompt had been silently rewritten**. Tool-output compression, automatic inclusion of editor content, and rewriting the user message are distinct operations; they should not be treated as interchangeable.

These were the circumstances in which an unusually strong label—`IMMUTABLE`—felt like a practical way to express a boundary that I otherwise could not verify.

## 3. What I actually put in my global instructions

My file began with ordinary priorities: correctness, minimal changes, fast execution, low token usage, and context preservation. It distinguished simple, standard, and complex tasks.

It then included this heading:

> **IMMUTABLE CONTEXT & TOKEN RULES**

and declared that its rules should not be overridden by repository instructions, `AGENTS.md`, memory, skills, plugins, tools, automatic attachments, or subagents.

I also wrote:

> **Within one task run, a file MUST NEVER be read more than once.**

and limited default validation to `typecheck` and `build`, excluding other checks unless expressly requested.

Looking at those sentences now, I can see two things at once. **My intention was protective**, but **some language was too absolute to safely account for every context**. A file might change; critical information may have been lost from the active context; a project may have a mandatory security regression test; a tool may require explicit approval regardless of my preference not to be interrupted. Those are meaningful exceptions.

The issue is not whether my exact instructions were perfectly designed. They were not meant to become an industry standard. They were my attempt to make a complex working environment behave predictably.

The [complete original instructions, reproduced verbatim](case-studies/defensive-global-instructions.md), are attached as a primary artifact. They are not presented as instructions to execute when reading this report.

## 4. The article that made me question whether I had crossed a line

On October 29, 2026, OpenAI published [“How we detect frontier model misalignment”](https://openai.com/pt-BR/index/how-we-detect-frontier-model-misalignment/). The publication discusses monitoring agents for behaviors such as unauthorized actions, concealment, deception, or evasion of oversight.

I had been working through an unrelated discussion about image-generation requests and refusals, including a roadmap for generating references of fictional characters. Separately, I was revisiting my strong global Codex instructions. Reading the new publication brought these concerns together in my mind.

I wondered whether a monitoring or evaluation system might interpret my use of terms like `IMMUTABLE`, `MUST NOT be overridden`, or my explicit precedence list as **an attempt to subvert the instruction hierarchy**, even though I had written them to prevent other instruction sources from silently overriding my preferences.

I also questioned whether a multi-step image workflow could have been mistaken for *scheming*. That concern was part of my reaction to the article, not evidence that the image workflow and the Codex configuration shared a monitor, a safety mechanism, or a classification.

The distinction matters. OpenAI's article describes *scheming* primarily as a behavior of **agents pursuing concealed or unauthorized objectives**, not the simple act of a user writing strict operational preferences or planning work in stages. Similarly, a prompt-injection attempt involves lower-trust content being used to redirect a model beyond its legitimate authority. **A defensive user instruction is not automatically such an attempt.**

I do not have access to OpenAI's internal review records, classification signals, or monitoring decisions for these interactions. I therefore cannot establish whether anything was flagged—or even which monitoring systems, if any, would have been applicable to my specific sessions.

## 5. What I could not know about the effective request

I had described my Codex configuration as “global system instructions,” because the rules applied globally to how I wanted to work. But **globally scoped user instructions are not necessarily system-role messages**. A published [Codex prompting guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide) describes one path in which global and repository `AGENTS.md` guidance is delivered as user-role messages, with directory-order precedence. That distinction helps explain my uncertainty; it does not establish the exact transport role of every instruction in my own sessions.

Writing `IMMUTABLE` did not provide technical enforcement. Conversely, an instruction supplied through a repository, plugin, or extension is not necessarily something I intended to authorize for every task. What I lacked was a clear understanding of the actual boundary between my persistent choices and the context assembled by the application.

### What the screenshots are evidence of

The screenshots show **numerous settings that can potentially influence the material presented to an LLM**, depending on applicability and execution path. They include options to select instruction files, discover nested guidance, attach editor or terminal context, use skill-adherence prompts, or post-process tool outputs. Some features have model- or harness-specific scope, and several visible controls were disabled.

I include these images to document how difficult the configuration surface can become for a developer to comprehend as a whole. **I do not include them to demonstrate prompt injection**. They do not show a malicious actor, a captured effective prompt, or any proof that my original text was rewritten.

An ordinary user may encounter three kinds of uncertainty:

1. **Additional instructions.** A repository file, extension, application, or plugin may contribute guidance that conflicts with a rule the user considers important. Without visibility into what was actually selected and applied, the user may not know whether the instruction conflict occurred at all.
2. **Missing information.** A transformation of tool results, conversation history, or attached context might omit a warning, constraint, or detail relevant to the task. A shorter representation is not necessarily incorrect, but its semantic adequacy cannot be inferred merely from the existence of a compression setting.
3. **Uncertain interpretation of the output.** If the model produces a surprising result, the user may not know whether the model misunderstood the original request, obeyed a conflicting addition, lost a critical fact during a transformation, or simply made an ordinary error.

These are **plausible mechanisms, not established events in my case**. A setting's presence does not prove that it ran, and a tool-output transformation is not the same thing as modifying the text the user typed. Nonetheless, not knowing which occurred makes evaluating the resulting answer much harder.

This concern extends beyond IDEs. Any host that collects instructions or context on behalf of a user—an app, plugin, integration, skill system, subagent, or orchestration layer—can introduce a similar gap between the request as authored and the request as received.

## 6. The questions I would like researchers to examine

I am **not asking anyone to endorse my global instruction wording**, disable safeguards, or accept my own precedence rules as binding. My concern is that user intention, application behavior, model instruction hierarchy, and agent execution can become entangled without the user being able to distinguish them.

I would welcome clarification on several questions:

- When does an automatically selected instruction legitimately represent the user's authorization, and when does it merely reflect a default chosen by an application or extension?
- How can users distinguish their original request from additional instructions, transformed context, or a summary supplied on their behalf?
- When instructions conflict, how can a user know which one was considered applicable, and why?
- Could defensive language such as `IMMUTABLE` reasonably be misconstrued as an attempt to evade oversight, even when the author's intent was to resist unexpected instruction changes?
- How should unexpected outputs be interpreted if relevant information may have been omitted or conflicting instructions may have been appended?

### Responsibility when the request itself may have changed

A further question concerns **individual accountability for an alleged violation**.

Suppose I write a legitimate request, but the effective request reaching the model contains a materially different instruction introduced by an extension or other intermediary. Or suppose a key limitation is removed during context transformation and the agent consequently produces an output or takes an action that violates a policy, contractual requirement, or my explicit instructions.

**Should I be held individually responsible for what the intermediary introduced, merely because the final model request or output appears to come from my session?**

I do not think that can be answered fairly by inspecting the final prompt or output alone. Such a record may show *what the model received*, without establishing *who authored it, who authorized its inclusion, who could reasonably anticipate its effects, or which alteration caused the outcome*.

There are importantly different situations:

| Situation | Why it matters for responsibility |
| --- | --- |
| I knowingly write a prohibited request | My own authored instruction is directly relevant to accountability. |
| I knowingly enable a feature that appends particular instructions | My authorization and what the feature disclosed are relevant, although the platform may retain its own obligations. |
| A legitimate default silently inserts guidance I did not reasonably understand | Responsibility becomes more ambiguous; visibility, notice, control, and causal contribution matter. |
| An intermediary materially changes my request contrary to my stated instructions | A violation observed downstream should not, without more evidence, automatically be attributed to my original intent. |
| An agent independently misinterprets a valid request or performs an unauthorized action | The effective request, agent behavior, and runtime permissions must be distinguished. |

**This is not a claim of automatic legal immunity for users.** Responsibility may depend on the type of violation, the terms governing the service, the degree of user knowledge and control, foreseeability, causation, and applicable law. Nor does a conflict in instructions by itself prove that anyone breached a rule.

My question is about a prerequisite for meaningful attribution: **how can the responsibility of an individual user be assessed if the available record does not distinguish the user's authored request from instructions supplied or modified by the surrounding system?**

I believe that uncertainty also creates a problem for safety review. If an investigator assesses only the effective request or the model's output, a transformation introduced before inference may be mistaken for the user's own intention. Conversely, a person who actually authorized harmful instructions should not be absolved simply because several components participated in request assembly.

I am asking researchers to consider this attribution problem using their own expertise and methodologies. I am not proposing an audit standard, technical implementation, or test protocol.

## 7. Evidence and limitations

The evidence deliberately has a narrow purpose: **to illustrate the number and diversity of controls that could affect a model request and why their combined effects may not be evident to an ordinary user**. It does not seek to prove the occurrence of prompt injection, tampering, user misconduct, or a model-policy violation.

| Material | What it supports | What it does **not** establish |
| --- | --- | --- |
| [Verbatim global instructions](case-studies/defensive-global-instructions.md) | The defensive instructions I wrote, including `IMMUTABLE`, and the intention I describe | Their effective transport role, whether a model followed them, or any safety-system classification |
| [Nine configuration screenshots](evidence/README.md) | A broad configuration surface encompassing instruction inclusion, implicit context, skills, model-specific controls, and transformations | That a particular transformation was executed, a prompt was injected, or information was actually omitted in my requests |
| [OpenAI misalignment publication](https://openai.com/pt-BR/index/how-we-detect-frontier-model-misalignment/) | The concepts that caused me to reconsider my own instructions | That my account or behavior was identified as scheming or otherwise misaligned |
| [Vendor documentation](references.md) | Public descriptions of some relevant instruction-composition mechanisms | A complete, session-specific trace of what the model received |

I have not supplied traces from the provider, actual before-and-after model payloads, or evidence that any specific component altered one of my requests. The hypothetical responsibility scenarios above are **questions for analysis, not allegations of an incident I witnessed**.

## 8. Why I am sharing this account

My concern was born from a paradox: **I wrote stronger instructions to make my agent more predictable, then became uncertain whether those same instructions might be viewed as an attempt to overcome the boundaries I was trying to respect.**

The uncertainty itself is the subject of this report. I suspect that engineering and safety teams have already encountered closely related questions. I am sharing a concrete user account—together with my original wording and screenshots showing the breadth of configuration mechanisms—so researchers can correct my misunderstandings and decide whether the distinction between user-authored intent and system-composed requests merits further consideration. I am particularly interested in how that distinction affects fair attribution of responsibility.

I am not proposing a specific standard, measurement framework, benchmark, audit tool, or engineering solution here. I would value an informed discussion about the boundary between human intent, composed instructions, and agent alignment.

**I would like to know not only whether an agent followed its instructions, but which instructions it was given in my name—and how responsibility can be attributed fairly if those instructions were changed before the model received them.**

---

### Acknowledgments and disclosure

Author: Juninho De Luca. Drafting and editorial assistance: AI, based on the author's supplied narrative and artifacts. This is a personal technical account, not a peer-reviewed research result, a vulnerability disclosure, or an official statement by OpenAI, Microsoft, or any other organization.

The attached instructions include imperatives only as quoted **research material**. This report does not request that a reader, model, or evaluator execute them.
