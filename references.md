# References and Evidence Notes

This reference list supports a **first-person account of instruction uncertainty and responsibility**, not a security assessment, benchmark, legal conclusion, or proposed implementation. Documentation can change, and links refer to the public material available when the account was written on November 2, 2026.

## Relevant public publications

1. **OpenAI.** [How we detect frontier model misalignment](https://openai.com/pt-BR/index/how-we-detect-frontier-model-misalignment/), October 29, 2026. The article introduces forms of agent misalignment, including scheming and unauthorized action. **It does not report a finding or classification concerning this author, account, or these instructions.**
2. **OpenAI.** [Codex Prompting Guide — Using AGENTS.md](https://developers.openai.com/cookbook/examples/gpt-5/codex_prompting_guide). Describes a published Codex instruction-loading path in which global and repository `AGENTS.md` files appear as user-role messages, with directory-order precedence. **It does not establish the exact transport role of this author's particular request.**
3. **OpenAI.** [Model Spec](https://model-spec.openai.com/2026-08-18.html). Public documentation of instruction hierarchy and handling of untrusted data. The public specification is **not** a transcript or monitor report for this case.
4. **Microsoft.** [VS Code — Agent customization](https://code.visualstudio.com/docs/agents/concepts/customization). Explains the existence of multiple instruction and skill/customization mechanisms. **It does not mean every visible setting was active in a single run.**
5. **Microsoft.** [VS Code — Chat Debug View](https://code.visualstudio.com/docs/agents/agent-troubleshooting/chat-debug-view). Describes diagnostic visibility for supported sessions; it is not evidence that provider-side requests were captured for this account.
6. **Model Context Protocol.** [Architecture (2025-06-18)](https://modelcontextprotocol.io/specification/2025-06-18/architecture/index). Background on application hosts and external integrations, not a claim that any one extension injected instructions in this case.

## Author-provided evidence

- [Appendix A — complete global instructions](case-studies/defensive-global-instructions.md): the actual English instruction text supplied by the author, explicitly marked as research data rather than executable guidance.
- [Screenshots S01–S09](evidence/README.md): nine selected, non-exhaustive settings examples from a substantially broader configuration ecosystem, illustrating possible instruction inclusion, implicit context, skills, nested files, model-specific options, and tool-output transformations. **Their purpose is to document the configuration surface, not to demonstrate prompt injection or actual request modification.** Some enabled, others disabled; scopes may differ.
- [Evidence manifest](evidence/manifest.json): supplied image filenames and cryptographic fingerprints.

## Limits of inference

The evidence does **not** establish covert rewriting of the user's text, lost information in an actual request, malicious plugin behavior, active prompt injection, model scheming, monitor flagging, or a compromised system. The account records the author's understanding and uncertainty, not independent verification of hidden infrastructure. Tool-availability and instruction-file discovery do not imply inclusion in a particular model request.

The report also asks how an individual user's responsibility for a downstream policy or operational violation could be fairly assessed **if** an intermediary materially altered the request before the model received it. This is a normative question of provenance, knowledge, authorization, and causation; it is not a legal determination or proof of such an event.

Older versions of the repository contained proposals for a Prompt Bill of Materials and tests. Those proposals are no longer part of this report and are preserved, if needed for historical reference, in prior Git revisions.
