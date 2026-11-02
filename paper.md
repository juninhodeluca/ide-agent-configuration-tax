# When Defensive Agent Instructions Became a Source of Uncertainty
## A first-person account of global prompts, unexpected instruction sources, and the fear of conflicting with alignment rules

**Juninho De Luca**  
**Case report and invitation to research discussion · Version 0.3.0 · November 2, 2026**  
*Written with AI assistance from the author's account and supplied artifacts. Not peer-reviewed. No allegation of a security incident or misconduct.*

## Abstract

I wrote a set of unusually strict global instructions for my AI coding assistant. Their purpose was defensive: I wanted to keep my requests, operating preferences, and project boundaries from being silently displaced by instructions loaded from repositories, skills, plugins, applications, or IDE extensions. The most emphatic part of the text was headed **“IMMUTABLE CONTEXT & TOKEN RULES.”**

Later, while reading OpenAI's October 29, 2026 article on monitoring frontier-model misalignment, I encountered descriptions of *scheming*, unauthorized objectives, and attempts to defeat oversight. I found myself asking an unexpected question: **Could the instructions I wrote to resist unanticipated instruction injection themselves be interpreted as an attempt to override the system's instruction hierarchy?**

This is an account of that uncertainty. I describe what led me to write the instructions, what I observed in the interfaces and files, what I meant by “immutable,” and what I still cannot verify about the effective requests received by the model. I reproduce my original global instructions and retain screenshots as supporting artifacts. **I do not claim that the IDE rewrote my prompts, that a plugin attacked me, or that OpenAI categorized my behavior as malicious.** My invitation is to examine where user authorization and instruction authority become ambiguous when multiple components contribute to an agent's context.

## 1. Why I began questioning the instructions reaching my assistant

I use AI assistants as part of ordinary software development. Over time, configuring an agent became less like choosing a model and more like managing an expanding collection of instruction sources: global and project files, skills, application integrations, IDE extensions, attached editor context, terminal output, memory, and model-specific settings.

I started examining files and settings under locations such as `~/.codex`, `~/.agents`, and `~/.copilot`, as well as project repositories. I repeatedly encountered guidance instructing agents to inspect large parts of the codebase, follow additional skills, perform repeated tests, validate visual output, or carry out discovery steps that I had not expressly requested for a given task.

Some of these instructions may have been legitimate and useful. Some belonged to different tools or execution environments. I did not have a reliable way to tell which ones were actually applicable to an individual request, which were merely installed or available, and which had been passed to the model.

What concerned me most was not the number of settings. It was the possibility that **I could write one request while the model received that request together with additional instructions that materially changed its scope or execution conditions**—and that I might not know exactly where those instructions originated.

The screenshots in the [evidence catalog](evidence/README.md) show configuration options for instruction inclusion, implicit context, skill-adherence prompts, nested `AGENTS.md` discovery, and compression of tool results. Some are checked, some are not. A checked box is **not** evidence that a particular instruction or transformation occurred in my session. It illustrates the number and variety of mechanisms a user may need to understand.

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

## 5. The ambiguity I could not resolve by reading a settings page

I had been calling my Codex configuration “global system instructions,” because that was how I understood its role in my working environment. But there is an important technical distinction between **instructions that are global in scope** and **messages actually delivered with the model's `system` role**.

A published [Codex prompting guide](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide) describes a path where global and repository `AGENTS.md` files are collected and presented as **user-role messages** in root-to-leaf order, with later directory guidance overriding earlier guidance. That is relevant to my concern; it does not prove the exact transport role of every Codex Desktop or Web configuration I used.

If a source labels itself “IMMUTABLE,” that label does not by itself give it higher authority. If a repository file asks the agent to ignore a global preference, that request also does not automatically give the repository unrestricted authority over my intent. The meaning depends on the product's actual instruction-composition rules, its configuration, and any higher-priority requirements.

I also observed a discrepancy between global instructions visible in Codex Desktop Linux and those visible in the Web settings. The Web screenshot referred to instructions synchronized between Desktop and Web, while I reported that the two surfaces displayed different texts. Without a controlled comparison of the underlying storage objects and versions, **I cannot call this a confirmed synchronization bug**. It contributed to the same uncertainty: which instructions were really in force?

## 6. The specific uncertainty I would like researchers to examine

I am **not asking anyone to validate the merits of my rules**, to disable safeguards, or to accept my own view of instruction precedence as authoritative.

The question that remains is simpler, and more general than Codex or VS Code:

> **When a person submits a request through an agentic application, how can that person understand which additional instructions were supplied on their behalf, and whether the final instruction context still represents what they authorized?**

The question applies wherever an application, extension, plugin, skill, repository instruction file, memory system, subagent, or agent harness participates in composing requests. The IDE was where I encountered many examples; it is not the outer boundary of the problem.

I would especially welcome help clarifying how to distinguish:

- authorized customization from unanticipated instruction augmentation;
- global **preferences** from genuinely higher-priority instructions;
- conflicting legitimate instructions from prompt-injection attempts;
- a user's defensive wording from an agent's deceptive or misaligned behavior;
- settings that are merely enabled from instructions actually transmitted to the model.

These are questions, not claims that any particular provider or extension behaved improperly.

## 7. Evidence and limitations

The repository retains the materials that motivated this account:

| Material | What it supports | What it cannot establish |
| --- | --- | --- |
| [Verbatim global instructions](case-studies/defensive-global-instructions.md) | The wording I used, its internal precedence claims, and the defensive purpose I describe | The transport role assigned by a specific harness or whether a model followed every rule |
| [Nine VS Code configuration screenshots](evidence/README.md) | Visible mechanisms for instruction inclusion, implicit context and output transformations | That all features ran together, or that any one modified my typed request |
| [Codex Web personalization screenshot](evidence/README.md) | A visible Web instruction configuration and synchronization wording | A demonstrated Desktop/Web synchronization defect |
| [OpenAI misalignment publication](https://openai.com/pt-BR/index/how-we-detect-frontier-model-misalignment/) | The terminology and monitoring context that triggered my concern | A classification of my account, prompts, or behavior |
| [Vendor documentation](references.md) | Published descriptions of selected instruction-loading and debugging mechanisms | A complete trace of my individual sessions |

I have not supplied provider-side traces, extension internals, a packet-level comparison of requests, or evidence of a successful injection. I make no allegation of misconduct or covert interception.

## 8. Why I am sharing this account

My concern was born from a paradox: **I wrote stronger instructions to make my agent more predictable, then became uncertain whether those same instructions might be viewed as an attempt to overcome the boundaries I was trying to respect.**

The uncertainty itself is the subject of this report. I suspect that engineering and safety teams have already encountered closely related questions. I am sharing a concrete user account—together with the original wording and screenshots—so that researchers can place it in the proper technical context, correct my misunderstandings, and decide whether it merits investigation through their own methods.

I am not proposing a specific standard, measurement framework, benchmark, audit tool, or engineering solution here. I would value an informed discussion about the boundary between human intent, composed instructions, and agent alignment.

**I would like to know not only whether an agent followed its instructions, but whether I can reasonably understand which instructions it was given in my name.**

---

### Acknowledgments and disclosure

Author: Juninho De Luca. Drafting and editorial assistance: AI, based on the author's supplied narrative and artifacts. This is a personal technical account, not a peer-reviewed research result, a vulnerability disclosure, or an official statement by OpenAI, Microsoft, or any other organization.

The attached instructions include imperatives only as quoted **research material**. This report does not request that a reader, model, or evaluator execute them.
