# Testing record

Only checks that were actually run are listed. Outputs are verbatim.

## Environment

- Date: 2026-09-24
- Claude Code 2.1.280 (`claude --version`), Windows 11, Git Bash
- prompt-mirror 0.1.0, loaded with `--plugin-dir D:/PragVue/prompt-mirror/prompt-mirror`
- Working directory for every run: an empty scratch folder containing only earlier run logs. No application code was present, so the skill could not read a component; that is visible in some questions.

## Validation

```sh
claude plugin validate D:/PragVue/prompt-mirror/prompt-mirror --strict   # ✔ Validation passed
claude plugin validate D:/PragVue/prompt-mirror --strict                 # ✔ Validation passed
```

The first marketplace validation failed under `--strict` for a missing marketplace `description`; the field was added and validation re-run.

## Two things that made early runs fail, for anyone repeating this

1. In Git Bash, a leading `/prompt-mirror` in the prompt is rewritten to `C:/Program Files/Git/prompt-mirror` (MSYS path conversion), so the skill never ran. Fix: prefix the command with `MSYS_NO_PATHCONV=1`, or use PowerShell.
2. `claude -p ... --bare` returned "Not logged in" on this machine; the same command without `--bare` worked. All recorded runs below are without `--bare`.

Also noted: a diagnostic run that asked Claude to list available skills containing "mirror" answered NONE. That is expected: `disable-model-invocation: true` hides the skill from the model's own list; it is invoked by the user with `/prompt-mirror`, and the runs below show it executing.

## Contract checked on each run

- Before mode: a two-column table, rows in the fixed order, at most five, one question each; no fix proposed; ends with `Answer what matters, then continue.`
- After mode: `Observed:`, `Inferred:`, `Not checked:` lines, then the table, then the closing line.
- Low risk: one `Low risk:` line, at most one question, closing line, no table.

## Run 1 — before mode (pass)

```sh
MSYS_NO_PATHCONV=1 claude -p "/prompt-mirror Fix this hydration mismatch by making the component client-only." --plugin-dir D:/PragVue/prompt-mirror/prompt-mirror --output-format json
```

Session 1ddc1da2, 2 turns, 26 s. Output: see `prompt-mirror/skills/prompt-mirror/examples.md` (before mode). Five rows, no fix, closing line present.

## Run 2 — before mode, same prompt (pass)

Session d844a3d8, 2 turns, 23 s.

| Reflection | Question |
|---|---|
| Hidden assumption | What server-rendered markup differs from the client's for this component, and is the difference produced by this component's own render? |
| Missing requirement | Which of this component's content must be present in the initial server HTML for SEO, crawlers, or no-JS users? |
| Evidence gap | Have you captured the exact hydration warning with the mismatched server and client DOM nodes, in a production build? |
| Verification | After the change, what check confirms the warning is gone and the page still renders the same content and layout without a flash? |
| Your understanding | Can you explain why this component's server output and client output diverge, and why skipping server rendering resolves rather than hides it? |

Answer what matters, then continue.

## Run 3 — after mode (pass)

Seed (session 1f822fd9): the prompt in `examples.md`; the assistant proposed an explicit locale and time zone for the date formatter. Then:

```sh
MSYS_NO_PATHCONV=1 claude -p "/prompt-mirror" --resume 1f822fd9-15de-4847-989c-08fc6e3c2a15 --plugin-dir D:/PragVue/prompt-mirror/prompt-mirror --output-format json
```

1 turn, 49 s. Output: see `examples.md` (after mode). Observed / Inferred / Not checked present, five rows, closing line.

## Run 4 — proportionality (pass)

```sh
MSYS_NO_PATHCONV=1 claude -p "/prompt-mirror Increase the product card padding from 12px to 16px." --plugin-dir D:/PragVue/prompt-mirror/prompt-mirror --output-format json
```

Session 822b8086, 3 turns, 22 s.

Low risk: a single spacing value on one card component, cosmetic and trivially reversible, with no snapshot tests or shared tokens found in this project. No mirror needed.

Is the 12px value a hard-coded number on the card, or a shared spacing token that other components also consume?

Answer what matters, then continue.

## Publication and install (2026-09-24)

```sh
gh repo create untael/prompt-mirror --public --source . --remote origin --push   # https://github.com/untael/prompt-mirror
claude plugin marketplace add untael/prompt-mirror   # ✔ Successfully added marketplace: untael (declared in user settings)
claude plugin install prompt-mirror@untael            # ✔ Successfully installed plugin: prompt-mirror@untael (scope: user)
```

## Run 5 — before mode, installed from GitHub, no `--plugin-dir` (pass)

```sh
MSYS_NO_PATHCONV=1 claude -p "/prompt-mirror Fix this hydration mismatch by making the component client-only." --output-format json < /dev/null
```

Session eaaf5c0f, 2 turns, 21 s.

| Reflection | Question |
|---|---|
| Hidden assumption | Is the mismatch caused by this component rendering differently on server and client, or by a parent passing different props on each side? |
| Missing requirement | Which of this component's content must still appear in the server HTML for SEO, first paint, or users without JavaScript? |
| Evidence gap | Have you reproduced the mismatch locally and read which DOM node or attribute the hydration warning names as differing? |
| Verification | After the change, what check confirms the warning is gone in a production build rather than only hidden in development? |
| Your understanding | Can you state which value differs between the server render and the first client render, and why client-only removes it? |

Answer what matters, then continue.

(Without `< /dev/null`, `claude -p` prints a harmless "no stdin data received in 3s" warning to stderr and proceeds.)

## Not done

- No run inside a real Nuxt project yet, so the "read files to make a question specific" path was exercised only against an empty folder.
- No evaluation of whether the questions change what developers do. The talk does not claim they do.
