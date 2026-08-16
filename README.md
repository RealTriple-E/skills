<p>
  <a href="https://github.com/RealTriple-E/skills">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="assets/elyazer-landscape-dark.jpg">
      <source media="(prefers-color-scheme: light)" srcset="assets/elyazer-landscape.jpg">
      <img alt="Elyazer Emmanuel — Skills" src="assets/elyazer-landscape.jpg" width="738">
    </picture>
  </a>
</p>

# Skills For Real Engineers

[![skills.sh](https://skills.sh/b/RealTriple-E/skills)](https://skills.sh/RealTriple-E/skills)

Agent skills for orchestration, UI design audit, and X/Twitter growth intelligence — built for real engineering, not vibe coding.

Developing real applications is hard. Approaches like GSD, BMAD, and Spec-Kit try to help by owning the process. But while doing so, they take away your control and make bugs in the process hard to resolve.

These skills are designed to be small, easy to adapt, and composable. They work with any model. They are based on real engineering experience. Hack around with them. Make them your own.

If you want to keep up with changes to these skills, and any new ones I create — watch the repo.

## Installation (30-second setup)

Two ways in, two philosophies. The Claude Code plugin installs the whole set as a managed, read-only bundle that updates when I ship. skills.sh copies editable skill files into your project, so you can hack on them and make them your own. Pick one.

### 1. Get the skills

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugins install elyazer-skills
```

Or, from inside a session:

```
/plugin install elyazer-skills
```

</details>

<details>
<summary><strong>Codex, and other agents</strong></summary>

```bash
npx skills@latest add RealTriple-E/skills
```

Pick the skills you want, and which coding agents to install them on.

</details>

<details>
<summary><strong>For tinkerers</strong></summary>

```bash
npx skills@latest add RealTriple-E/skills
```

It writes the skills into your repo as ordinary files you own and can edit. Pull my latest changes when you want them with `npx skills update`.

</details>

### 2. Run the setup command

In your agent, run the setup command for the skill you want. Each skill is self-contained — read its SKILL.md for invocation details.

### 3. Bam — you are ready to go.

## The Skills

---

### [duckswarm](skills/orchestration/duckswarm/SKILL.md)

**Multi-model debate and consensus orchestration via Duck.ai.**

Duckswarm turns the local (weaker) model into a high-quality conductor that recruits, debates, and synthesizes stronger models available on Duck.ai. The local model never invents facts — it only plans, routes, critiques, and recombines.

**What it does:**

- Splits hard problems into atomic claims that can be verified independently
- Runs multi-round debate between models from Duck.ai — Claude-family, GPT-family, and strong open models — all through Duck.ai's zero-auth browser interface
- Scores every claim by consensus confidence and divergence, surfacing only what the models agree on
- Produces a structured report: verified core answer, supporting evidence map, model divergence matrix, residual uncertainties, and recommended next action
- Works on coding, math, research, vision, reasoning, architecture, debugging, planning, and any high-stakes problem
- Falls back gracefully when Duck.ai is unreachable — never hallucinates a substitute

**When to use it:** any non-trivial coding, research, vision, math, reasoning, or high-stakes problem. Also trigger on: `duckswarm`, `consensus`, `multi-model`, `cross-check`, `amplify this`, `debate this`, `verify across models`, `duck.ai consensus`, `frontier-level answer`.

**Author:** Elyazer Emmanuel · **Version:** 1.1

---

### [unvibecode-ui](skills/engineering/unvibecode-ui/SKILL.md)

**Frontend UI audit and unvibecoding — from generic interface to deliberate product.**

Act as a senior product designer, frontend architect, and accessibility reviewer. Turn a functional but generic interface into a deliberate, coherent product interface.

**What it does:**

- Scans every screen — modals, drawers, auth, onboarding, loading, empty, error, and detail states — building a full inventory before touching a single line of CSS
- Detects vibe-coded signals: generic typography, unexamined icon defaults, blue/purple gradients, card-within-card structures, low-contrast gray-on-gray text, identical radii everywhere, missing states, and the long tail of AI-generated UI patterns
- Reconstructs the design language: brand personality, visual grammar, typography scale, semantic color roles, spacing scale, radius scale, elevation strategy, icon conventions, responsive rules, and motion language
- Scores every screen across 12 dimensions (hierarchy, layout, spacing, typography, color, consistency, responsive, accessibility, states, density, distinctiveness) with weighted rationale
- Produces one global redesign direction before any screen rewrites — what to stop, what to keep, what to introduce, 5–8 operational design principles, proposed tokens, shared component changes, responsive rules, and product identity strategy
- Outputs screen-by-screen rewrite commands — concrete implementation instructions another coding agent can execute without making unbounded aesthetic guesses
- Rebuilds the shared system (tokens, primitives) before mass-editing screens
- Implements in controlled passes: foundation → highest-impact screens → shared patterns → real states → responsive → visual QA
- Accessibility baseline: WCAG 2.2 — semantic controls, keyboard access, visible focus, contrast, resize/reflow, target size, meaningful headings, error recovery

**When to use it:** when an interface works but looks generic, inconsistent, templated, AI-generated, unfinished, or visually unprofessional. Or when asked to redesign/refactor frontend screens without changing core product functionality.

**Author:** Elyazer Emmanuel · **Version:** 1.0.0 · **License:** MIT

---

### [x-growth-intelligence](skills/growth/x-growth-intelligence/SKILL.md)

**X/Twitter growth intelligence — research, strategy, content, publishing, and analytics.**

An experienced X strategist operating as an agent skill. Research, strategize, create, optimize, publish (via browser session), engage, analyze, and improve content for any account. Never behaves like a generic tweet generator.

**What it does:**

- Populates strategy from a runtime Account Profile — never hard-codes a niche or brand
- Determines the active Objective first — strategy changes with the objective
- Runs Trend Detection → Relevance Filter → classify opportunity (NOW / TODAY / THIS WEEK / EVERGREEN / AVOID)
- Applies Algorithm Intelligence + Recommendation Eligibility before finalizing any post
- Drafts with Human Writing Engine + Voice DNA + Brand Guardrails on every post
- Enforces 11 quality gates: strategic relevance, audience relevance, originality, hook strength, value, conversation potential, algorithm-informed quality, brand safety, voice consistency, spam check, and final human-quality test
- Manages the full content lifecycle on a Hermes Kanban board when available
- Uses a persistent encrypted browser session for publishing — no paid API required. Only the Publisher role loads the session
- Supports four autonomy levels: Manual (draft only), Assisted (research + draft + timing), Approval (prepare everything, wait for human confirm — default safe mode), Autonomous (research, publish, engage, analyze inside guardrails)
- Labels every strategic claim: CONFIRMED / SUPPORTED / EXPERIMENTAL / SPECULATIVE
- Rate discipline: irregular human-like intervals, hard daily caps, circuit-breaker on friction signals
- Dry-run mode: produce full structured output without loading the session or publishing

**When to use it:** X growth, Twitter strategy, content planning, post drafting, trend analysis, reply intelligence, campaign management, account health, or when managing any X account via Account Profile.

**Author:** Elyazer Emmanuel · **Version:** 1.0.0 · **License:** MIT

---

## Why These Skills Exist

### #1: The Agent Did Not Do What I Want

> "No-one knows exactly what they want"
> — David Thomas & Andrew Hunt, *The Pragmatic Programmer*

The most common failure mode in software development is misalignment. You think the dev knows what you want. Then you see what they built — and realise it did not understand you at all. This is just the same in the AI age. The fix is a **grilling session** — getting the agent to ask detailed questions before building.

### #2: The Agent Is Way Too Verbose

> With a ubiquitous language, conversations among developers and expressions of the code are all derived from the same domain model.
> — Eric Evans, *Domain-Driven Design*

At the start of a project, devs and domain experts usually speak different languages. Agents are dropped into a project and asked to figure out the jargon as they go — so they use 20 words where 1 will do. The fix is a shared language. These skills establish deliberate process and shared vocabulary so the agent knows exactly what you want.

## License

MIT — see [LICENSE](LICENSE).
