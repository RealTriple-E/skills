# Research Basis

This skill was designed after reviewing current guidance and practice around Agent Skills, responsive/adaptive layout, accessibility, design systems, and the specific failure modes commonly reported for vibe-coded interfaces.

## Agent Skill format

- Agent Skills specification: https://agentskills.io/specification
- GitHub Copilot skills: https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills
- Claude Code skills: https://code.claude.com/docs/en/skills

Why it matters: the skill uses the portable `SKILL.md` format and keeps detailed references outside the main instruction file so agents can load them progressively.

## Accessibility

- WCAG 2.2: https://www.w3.org/TR/WCAG22/

Relevant guidance includes focus visibility/not obscured, target size, contrast, reflow, semantic relationships, and accessible authentication.

## Adaptive layout and information hierarchy

- Android adaptive layout guidance (2026): https://developer.android.com/design/ui/mobile/guides/layout-and-content/adapt-layout
- Android content composition and structure: https://developer.android.com/design/ui/mobile/guides/layout-and-content/content-structure
- Android layout/navigation patterns: https://developer.android.com/design/ui/mobile/guides/layout-and-content/layout-and-nav-patterns

The useful principles are broader than Android: use meaningful grids/containers, align related content, constrain excessive stretching, let layouts reflow or change presentation, and choose navigation based on size and information architecture.

## Typography and accessibility

- Apple Human Interface Guidelines — Typography: https://developer.apple.com/design/human-interface-guidelines/typography/
- Apple Human Interface Guidelines — Accessibility: https://developer.apple.com/design/human-interface-guidelines/accessibility/

Relevant principles include legibility, limiting unnecessary typeface variation, maintaining hierarchy, supporting larger text, and avoiding overly thin type for small text.

## Accessible component primitives

- Radix Primitives — Introduction: https://www.radix-ui.com/primitives/docs/overview/introduction
- Radix Primitives — Accessibility: https://www.radix-ui.com/primitives/docs/overview/accessibility

These reinforce the value of reusable, accessible primitives with correct focus management, keyboard interaction, roles, and semantics.

## AI-ready open-code component systems

- shadcn/ui: https://ui.shadcn.com/docs
- shadcn/ui component composition guidance: https://ui.shadcn.com/docs/changelog/2026-04-component-composition
- shadcn/ui style customization: https://ui.shadcn.com/docs/changelog/2025-12-shadcn-create

Relevant principles: predictable composable structures are easier for agents to inspect and modify; beautiful defaults are useful, but customization is essential when a product needs a distinct identity; composition guidance helps agents preserve correct component structure.

## Current discussion of vibe-coded UI

The following practitioner/community sources were reviewed to identify recurring patterns. They are treated as observational evidence, not normative standards:

- The Crit — "Why Your Vibe-Coded App Looks Like Every Other AI App": https://thecrit.co/resources/vibe-coding-design-guide
- Differ — "Design Tips for your Vibe Coded Project": https://blog.getdiffer.com/design-tips-vibe-coded-project
- Element Armory — "How to Vibe Code UI Without Getting Stuck": https://elementarmory.com/blog/vibe-code-ui
- Reddit community discussion on professional frontend workflows: https://www.reddit.com/r/vibecoding/

Recurring observations include default typography/icon choices, overuse of rounded cards and gradients, generic dashboard compositions, token inconsistency, and the need to treat AI as an implementation partner constrained by explicit design decisions rather than as an unconstrained designer.

## Interpretation

This skill does not define one visual style. It defines a method for discovering and enforcing a product-specific style while preserving usability, accessibility, and maintainability.
