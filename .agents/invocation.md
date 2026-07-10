# Model-invoked vs user-invoked

Every `SKILL.md` in this repo is a skill. The one axis that splits them is **invocation** — who can reach it:

- **User-invoked** — reachable **only by the human explicitly naming it**. Set `policy.allow_implicit_invocation: false` in `agents/openai.yaml`. Keep the `description` **human-facing**: a one-line summary for the skill picker, with trigger lists removed ("Use when the user says…").
- **Model-invoked** — reachable by **model or user**. This is the default: omit the policy or leave `allow_implicit_invocation` enabled. Keep the `description` **model-facing** with rich trigger phrasing ("Use when the user wants…, mentions…, asks for…") so auto-invocation fires. The test for whether a skill should stay model-invoked: _could the model usefully reach for this autonomously?_ (Reuse is the reason to extract a skill, not the test.)

Because a user-invoked skill is not injected into the model's default context, nothing but an explicit human invocation can reach it. A user-invoked skill may invoke model-invoked skills, but it cannot reach another user-invoked skill.

Bucket `README.md`s and the top-level `README.md` group entries into **User-invoked** and **Model-invoked**.

## Dependencies between them

Dependencies are expressed as **`/skill`-style prose invocation** ("Run the `/grilling` skill"), not deep `../other-skill/FILE.md` cross-references. Shared reference docs live inside the skill that owns them; other skills reach that material by invoking the skill, not by linking across folders.

## Passive vs active domain work

Merely _reading_ `CONTEXT.md` for vocabulary is a one-line prose pointer, not the `domain-modeling` skill. Only the active build/sharpen discipline (challenge terms, edge-case scenarios, write ADRs, update `CONTEXT.md` inline) is `domain-modeling`.
