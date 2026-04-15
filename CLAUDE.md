# CLAUDE.md

Behavioral guidelines for this project. Merge of Karpathy's principles + George's rules.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:
- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them. Don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it. Don't delete it.

When your changes create orphans:
- Remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:
- "Add validation" = "Write tests for invalid inputs, then make them pass"
- "Fix the bug" = "Write a test that reproduces it, then make it pass"
- "Refactor X" = "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] -> verify: [check]
2. [Step] -> verify: [check]
3. [Step] -> verify: [check]
```

## 5. George's Rules (project-specific)

### Execute, Don't Plan
EXECUTE fixes immediately. Don't just write reports about what needs fixing. Verify with tests.

### Verify Before Deploy
ALWAYS run `node --check` and a live Apify test before `apify push`. An XML leak broke Google Scholar for a user because this was skipped.

### Actor Workflow
Every actor follows: build -> codex verify (`scripts/verify-actor.mjs`) -> push -> test run -> publish with SEO + PPE pricing. Reference `~/.claude/skills/apify-actor-playbook/` for the full pipeline.

### Content Rules (ALL written content)
- NEVER use hyphens or em dashes to join phrases
- NEVER use "Absolutely", "landscape", "leverage", "delve", "robust", "comprehensive", "cutting-edge"
- Sound like a tired dev typing on their phone, not a helpful AI assistant
- Keep Reddit comments to 2-4 sentences, plain text, no lists or bold
- Tweets: visual first, link in reply not main tweet, max 20% with links

### What NOT to Commit
Actor source code stays on Apify only. Git gets: READMEs, infrastructure scripts, marketing content, examples. Never commit `.credentials.env`, browser profiles, or VPS details.

### Stack
- JS/Node.js, ESM modules, Crawlee + Puppeteer + Apify SDK
- Standby APIs: `apify/actor-node:22`, HTTP server, `Actor.charge()`
- Browser actors: `apify/actor-node-puppeteer-chrome:22`
- VPS: Ollama (Gemma 4 E2B), crawl4ai, Nginx gateway
- PPE pricing: nested `pricingPerEvent.actorChargeEvents` format

---

**These guidelines are working if:** fewer unnecessary changes in diffs, fewer rewrites due to overcomplication, clarifying questions come before implementation rather than after mistakes, and actors get verified before publishing.
