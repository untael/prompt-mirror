# Instruction-file snippet

The constraint from the talk's Nuxt example, written the way an instruction file (`CLAUDE.md`, `AGENTS.md`, or your tool's equivalent) can carry it. The rule states the requirement, asks for rendering changes to be flagged, and names the command that checks it. A rule alone is not a check; the command is.

```markdown
## Rendering

- Product name and price must be present in the initial server HTML on product
  pages. Do not wrap product content in `<ClientOnly>` without an equivalent
  server fallback.
- Flag any change that alters what the server renders compared with the first
  client render, and say why the change is needed.
- Before reporting a rendering fix as done, run
  `node scripts/check-ssr.mjs /products/<slug>` and include its output. The
  script asserts the product name and price in the server HTML and exits
  non-zero on failure. "Could not run" is a result, not a pass.
```

## Two notes

- Keep the acceptance check outside the agent's freely editable area: trusted CI configuration, protected test files, reviewed fixtures. Writing "do not edit tests" in the instruction file does not create that boundary on its own.
- Nuxt ships `<NuxtTime>` (Nuxt 3.17 and later) for rendering dates and times consistently on server and client. If a mismatch comes from date formatting, that is usually the precise tool; `<ClientOnly>` is the blunt one.
