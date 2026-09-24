# Prompt Mirror

Five questions before you accept the change.

A small Claude Code skill that reflects your request, or the agent's last proposal, back at you: the hidden assumption, the missing requirement, the evidence gap, the check that would demonstrate success, and whether you can explain the fix. It never proposes the fix. You still do the investigating.

Built for the PragVue 2026 talk **AI Development Tips: Your AI Agrees With You. That's the Problem.** by Pavel Mironov (Epicmax). The talk's companion material is in [`talk/`](talk/).

## Install

Inside Claude Code:

```text
/plugin marketplace add untael/prompt-mirror
/plugin install prompt-mirror@untael
```

From a shell:

```sh
claude plugin marketplace add untael/prompt-mirror
claude plugin install prompt-mirror@untael
```

Without the plugin system, copy `prompt-mirror/skills/prompt-mirror/` into `~/.claude/skills/` (all projects) or `.claude/skills/` (one project).

## Use

```text
/prompt-mirror Fix this hydration mismatch by making the component client-only.
```

Pass a request before a consequential change. Run `/prompt-mirror` with no argument after the agent has proposed something, and it reflects on that proposal, separating what was observed from what was inferred and what was not checked.

It never runs on its own, so it will not interrupt a padding tweak. Requests it judges low risk get a single line instead of the table. Reflection effort should match the risk.

## Example

Recorded on 2026-09-24 with Claude Code 2.1.280 and prompt-mirror 0.1.0, verbatim:

| Reflection | Question |
|---|---|
| Hidden assumption | Why is this component the source of the mismatch, rather than a parent, a browser extension, or data that differs per request? |
| Missing requirement | Which of the component's content must still appear in the server-rendered HTML for SEO, first paint, or users without JavaScript? |
| Evidence gap | Have you compared the server HTML and the first client render for this component to see which node or attribute differs? |
| Verification | Which check proves the mismatch warning is gone in a production build and the component's layout does not shift when it mounts? |
| Your understanding | Can you explain what in this component produces different output on the server than in the browser, and why skipping server rendering removes it? |

Answer what matters, then continue.

More runs, including the after-mode output, are in [`prompt-mirror/skills/prompt-mirror/examples.md`](prompt-mirror/skills/prompt-mirror/examples.md). What was tested and how is in [`TESTING.md`](TESTING.md).

## What it does not do

- It does not propose, sketch or apply a fix.
- It does not answer its own questions.
- It does not guarantee anything. Its output is fallible; it can surface a question you missed, and you still need to investigate the answer.

## Talk companion

- [`talk/checklist.md`](talk/checklist.md): the five questions as a plain checklist, plus the three closing questions.
- [`talk/claude-md-snippet.md`](talk/claude-md-snippet.md): the instruction-file snippet from the talk's Nuxt example.
- [`talk/prompts.md`](talk/prompts.md): the investigation prompt, the check-script prompt and the four rules for trusting a check.
- [`talk/references.md`](talk/references.md): research references with their limits, and technical links.

## Licence

MIT. See [LICENSE](LICENSE).
