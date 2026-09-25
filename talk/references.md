# AI Development Tips — references

*Your AI Agrees With You. That's the Problem.* — Pavel Mironov, Epicmax. PragVue 2026, Prague, 29 September 2026.

Some points in the talk come from experiments, some from surveys, and some are practical interpretations applied to frontend work. Each entry states its limits.

## Research

1. **Herbert A. Simon (1992). What Is an "Explanation" of Behavior?** *Psychological Science*, 3(3), 150–161. Quotation on printed p. 157: "Most often, a stop rule halts the search when a satisfactory alternative is found—one that meets a variety of criteria but maximizes none."
   [Original article in the Carnegie Mellon University archive](https://iiif.library.cmu.edu/file/Simon_box00069_fld05358_bdl0001_doc0001/Simon_box00069_fld05358_bdl0001_doc0001.pdf)
   Used on slide 6. Supports the satisficing explanation; applying it to fast AI answers is the talk's interpretation.

2. **Sharma et al. (2023; ICLR 2024). Towards Understanding Sycophancy in Language Models.**
   [Paper](https://arxiv.org/abs/2310.13548)
   Used on slide 5. Five assistants evaluated; preference data found to favour responses that match the user's views. Evidence about the assistants and conditions studied, not a universal claim about current models.

3. **Reber & Schwarz (1999). Effects of Perceptual Fluency on Judgments of Truth.** *Consciousness and Cognition*, 8(3), 338–342.
   [Abstract and DOI](https://pubmed.ncbi.nlm.nih.gov/10487787/)
   Used on slide 7. Manipulates visual readability; does not directly test LLM formatting, confidence, or punctuation.

4. **Shen & Tamkin (2026). How AI Impacts Skill Formation.** Anthropic, 29 January 2026.
   [Authors' research report and link to the paper](https://www.anthropic.com/research/AI-assistance-coding-skills)
   Used on slide 9. Randomised coding study, 52 mostly junior developers, unfamiliar Python library (Trio), immediate quiz: 50 % with AI versus 67 % without, a 17 percentage-point gap (authors report Cohen's d = 0.74, p = 0.01). The AI group finished about two minutes faster, not statistically significant. Usage-pattern analysis is observational.

5. **Lee et al. (2025). The Impact of Generative AI on Critical Thinking: Self-Reported Reductions in Cognitive Effort and Confidence Effects From a Survey of Knowledge Workers.** CHI 2025.
   [CHI paper](https://doi.org/10.1145/3706598.3713778)
   Used on slide 9. Survey of 319 knowledge workers, 936 examples; associations and self-reports, not a causal demonstration of skill decline.

6. **Buçinca, Malaya & Gajos (2021). To Trust or to Think: Cognitive Forcing Functions Can Reduce Overreliance on AI in AI-assisted Decision-making.** CSCW 2021.
   [Paper](https://arxiv.org/abs/2102.09692)
   Used on slide 14. Decision-making experiment with 199 participants; supports deliberate engagement. Participants rated the most effective interventions least favourably. Not a direct evaluation of Prompt Mirror or a coding workflow.

## Technical references

- [Nuxt: ClientOnly](https://nuxt.com/docs/3.x/api/components/client-only). Server-build behaviour of the default slot and the option of server fallbacks. Slides 4 and 8.
- [Nuxt: Hydration best practices](https://nuxt.com/docs/4.x/guide/best-practices/hydration). Background for the illustrative rendering scenario; its worked solution for date and time output is `<NuxtTime>`.
- [Nuxt: NuxtTime](https://nuxt.com/docs/4.x/api/components/nuxt-time). Renders dates and times consistently on server and client; available since Nuxt 3.17. Slide 4.
- [Claude Code: Memory and CLAUDE.md](https://code.claude.com/docs/en/memory)
- [Claude Code: MCP](https://code.claude.com/docs/en/mcp)
- [Claude Code: Skills](https://code.claude.com/docs/en/skills)
- [Claude Code: Subagents](https://code.claude.com/docs/en/sub-agents)
- [Claude Code: Plugins](https://code.claude.com/docs/en/plugins). How Prompt Mirror is packaged.
- [Anthropic: Skills explained](https://claude.com/blog/skills-explained). Background for the capability distinctions on slides 3 and 11.
- [evidence-layer (npm)](https://www.npmjs.com/package/evidence-layer). Inspiration for slide 12: turning "verified" into a claim that could be proved wrong, and treating "unverifiable" as distinct from a pass. Ideas only; the package was not used or evaluated for this talk.

## Illustrations and attribution

- Slide 10 quotes Barbossa in *Pirates of the Caribbean: The Curse of the Black Pearl* (2003): "the code is more what you'd call 'guidelines' than actual rules." The film still shows the Pirate Code book from *At World's End* (2007).
- The car and supercar comparison on slide 2 is a teaching analogy about amplification. It makes no claim about anyone's driving or about the difficulty of any technological transition.
- The agent turns on slides 4, 5, 7 and 8, the Nuxt scenario and the check-ssr output on slide 12 are scripted illustrations. The answer-ordering and recommendation examples are observations to discuss, not quantified findings from the cited studies.
- [Claude Code: Hooks](https://code.claude.com/docs/en/hooks) is the reference for the Stop hook mentioned on slide 12.
- Prompt Mirror v0.1 exists in this repository. The output on slide 13 is a recorded run (see `prompt-mirror/skills/prompt-mirror/examples.md`). The skill has not been evaluated experimentally.
