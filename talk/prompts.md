# Prompts from the talk

Copy, adapt, use. They are written for the talk's Nuxt product-card example; swap in your own component and requirement.

## Investigate before implementing

> Investigate the hydration mismatch. Preserve product content in server HTML. Compare the server and initial client output before proposing a change.

Say what must remain true, record your hypothesis as a hypothesis, and let the agent find the cause before it touches the code.

## Ask for a tool, not an opinion

> Write a script that requests the product page from the server build, before any JavaScript runs, and asserts the product name and price in the rendered HTML. Record the commit and command. Exit non-zero on failure.

Four rules that make the script's output worth trusting:

1. Decide in advance what would count as failure.
2. "Couldn't run" is its own result, never a pass.
3. Watch the check fail once before you trust it.
4. Every "verified" points to the run that produced it.

## Reflect at the decision point

```text
/prompt-mirror Fix this hydration mismatch by making the component client-only.
```

Before a consequential change: pass the request. After the agent has proposed something: run `/prompt-mirror` with no argument and it reflects on that proposal, separating what was observed from what was inferred.

## Ask for a reviewer, not a persona

> Identify changes to server output and the initial client render. Support findings with file references and test evidence.

A reviewer role directs attention to a question and asks for evidence. A title such as "world-class frontend engineer" does neither.
