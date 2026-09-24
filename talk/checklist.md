# Five questions before you accept the change

The same five reflections Prompt Mirror produces, as a plain checklist for when you are not in Claude Code. Answer what matters, then continue.

- [ ] **Hidden assumption.** What does this request take for granted? In the talk's example: that client-side rendering is acceptable for this component.
- [ ] **Missing requirement.** What must stay true that nobody wrote down? Example: product name and price must appear in the initial server HTML.
- [ ] **Evidence gap.** What has not been observed or reproduced yet? Example: why the server and the browser rendered different text.
- [ ] **Verification.** Which independent check would demonstrate success? Example: request the page from the server build and assert the name and price in the rendered HTML before any JavaScript runs.
- [ ] **Your understanding.** Can you explain why the proposed fix works, and under what conditions it would fail?

## Three questions for the next tool

- What am I assuming?
- What evidence supports this change?
- Can I explain why it works?

## One test for tomorrow

Could I debug this tomorrow if the chat disappeared? If not, that is where attention still needs to go.
