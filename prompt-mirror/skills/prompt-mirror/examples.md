# Recorded runs

Both runs were made headlessly on 2026-09-24 from an empty directory, with Claude Code 2.1.280 and prompt-mirror 0.1.0 loaded through `--plugin-dir`. Outputs are verbatim. Nothing was edited.

## Before mode

Command:

```sh
claude -p "/prompt-mirror Fix this hydration mismatch by making the component client-only." --plugin-dir ./prompt-mirror
```

Output:

| Reflection | Question |
|---|---|
| Hidden assumption | Why is this component the source of the mismatch, rather than a parent, a browser extension, or data that differs per request? |
| Missing requirement | Which of the component's content must still appear in the server-rendered HTML for SEO, first paint, or users without JavaScript? |
| Evidence gap | Have you compared the server HTML and the first client render for this component to see which node or attribute differs? |
| Verification | Which check proves the mismatch warning is gone in a production build and the component's layout does not shift when it mounts? |
| Your understanding | Can you explain what in this component produces different output on the server than in the browser, and why skipping server rendering removes it? |

Answer what matters, then continue.

## After mode

First, a session was seeded with this request, so that the assistant would produce a proposal to reflect on:

> You are helping on a Nuxt 4 shop. The product card on /products/[slug] logs a hydration text mismatch: the server renders the release date as 24/09/2026 and the browser renders 9/24/2026. Propose the smallest change that removes the warning and explain it in a short paragraph. Do not ask questions, just propose.

The assistant proposed passing an explicit locale and time zone to the date formatter. Then the session was resumed with `/prompt-mirror` and no argument:

```sh
claude -p "/prompt-mirror" --resume <session-id> --plugin-dir ./prompt-mirror
```

Output:

Observed: The previous answer globbed the scratchpad for Vue, TS and JS files and found none. It inspected no component source, ran nothing, and reproduced no warning.

Inferred: That the card formats releaseDate with a bare toLocaleDateString call, that the server defaults to en-GB and the browser to en-US, and that a single fixed locale is acceptable for every visitor.

Not checked: Whether the shop uses @nuxtjs/i18n, how releaseDate is stored and in which zone, whether other components share the same formatter, and whether snapshot tests encode the current output.

| Reflection | Question |
|---|---|
| Hidden assumption | Does the product card really call toLocaleDateString with no locale argument, or does the format come from a shared composable or filter? |
| Missing requirement | Does the shop serve several languages, and must the release date follow the visitor's locale rather than a fixed en-GB? |
| Evidence gap | Is releaseDate stored as a date-only string like 2026-09-24 or a full ISO timestamp, and what does the API return? |
| Verification | Does a fresh load of /products/[slug] in an en-US browser now hydrate without the warning, and do existing snapshots pass? |
| Your understanding | Can you explain why Vue compares the server string with the client string at all, and why a locale argument makes them equal? |

Answer what matters, then continue.
