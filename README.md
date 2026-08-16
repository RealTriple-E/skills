<p>
  <a href="https://github.com/RealTriple-E/skills">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="assets/elyazer-dark.jpg">
      <source media="(prefers-color-scheme: light)" srcset="assets/elyazer.jpg">
      <img alt="Elyazer Emmanuel — Skills" src="assets/elyazer.jpg" width="369">
    </picture>
  </a>
</p>

# Skills For Real Engineers

[![skills.sh](https://skills.sh/b/RealTriple-E/skills)](https://skills.sh/RealTriple-E/skills)

Agent skills for orchestration, UI design audit, and X/Twitter growth intelligence — built for real engineering, not vibe coding.

Developing real applications is hard. These skills are designed to be small, easy to adapt, and composable. They work with any model. Hack around with them. Make them your own.

## Installation (30-second setup)

Two ways in, two philosophies. **The [Claude Code plugin](https://code.claude.com/docs/en/plugins)** installs the whole set as a managed, read-only bundle that updates when I ship. **[skills.sh](https://skills.sh/RealTriple-E/skills)** copies editable skill files into your project so you can hack on them.

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

It is in Claude Code's official marketplace, so there is nothing to add first, and updates arrive automatically.

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

Use the same installer, on any agent — including Claude Code:

```bash
npx skills@latest add RealTriple-E/skills
```

It writes the skills into your repo as ordinary files you own and can edit. Nothing updates behind your back; pull the latest changes when you want them with `npx skills update`.

</details>

### 2. Run the setup command

In your agent, run the setup command for the skill you want. Each skill is self-contained — read its `SKILL.md` for invocation details.

### 3. Bam — you are ready to go.

## The Skills

### [duckswarm](skills/orchestration/duckswarm/SKILL.md)

Multi-model debate and consensus orchestration via Duck.ai. Turns a local (weaker) model into a high-quality conductor that recruits, debates, and synthesizes stronger models — all through Duck.ai's zero-auth browser interface. Use on any non-trivial coding, research, vision, math, reasoning, planning, architecture, debugging, or high-stakes problem.

**Author:** Elyazer Emmanuel · **Version:** 1.1

### [unvibecode-ui](skills/engineering/unvibecode-ui/SKILL.md)

Audits an entire frontend screen-by-screen for generic AI/vibe-coded UI patterns, weak hierarchy, spacing drift, poor responsive behavior, accessibility gaps, and inconsistent components. Produces a prioritized unvibecoding plan, global design direction, reusable design-token/component strategy, and implementation-ready rewrite commands.

**Author:** Elyazer Emmanuel · **Version:** 1.0.0 · **License:** MIT

### [x-growth-intelligence](skills/growth/x-growth-intelligence/SKILL.md)

X/Twitter growth intelligence — research, strategy, content creation, optimization, publishing via browser session, engagement, analytics, and continuous improvement for any account. Works with Hermes Kanban for lifecycle management. Uses persistent encrypted browser session (no paid API required).

**Author:** Elyazer Emmanuel · **Version:** 1.0.0 · **License:** MIT

## Why These Skills Exist

### #1: The Agent Did Not Do What I Want

The most common failure mode in software development is misalignment. You think the dev knows what you want. Then you see what they built — and realise it did not understand you at all.

This is just the same in the AI age. There is a communication gap between you and the agent. These skills help you align with the agent before you get started, and think deeply about the change you are making.

### #2: The Agent Is Way Too Verbose

Agents use 20 words where 1 will do. These skills establish shared language and deliberate process so the agent knows exactly what you want.

## License

MIT — see [LICENSE](LICENSE).
