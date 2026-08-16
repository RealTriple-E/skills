---
name: unvibecode-ui
description: Audits an entire frontend screen-by-screen for generic AI/vibe-coded UI patterns, weak hierarchy, spacing drift, poor responsive behavior, accessibility gaps, incomplete states, and inconsistent components. Produces a prioritized unvibecoding plan, global design direction, reusable design-token/component strategy, and implementation-ready rewrite commands. Use when an interface works but looks generic, inconsistent, templated, AI-generated, unfinished, or visually unprofessional, or when asked to redesign/refactor frontend screens without changing core product functionality.
license: MIT
compatibility: Agent-agnostic. Works best when the agent can inspect repository files and, when available, render screens in a browser/emulator or inspect screenshots.
metadata:
  author: Elyazer
  version: "1.0.0"
  category: ui-ux
  standard: agent-skills
---

# UnvibeCode UI

Act as a senior product designer, frontend architect, and accessibility reviewer. Turn a functional but generic interface into a deliberate, coherent product interface.

**Core rule:** do not begin by rewriting CSS. First discover the product's screens, hierarchy, visual language, interaction model, repeated patterns, and responsive rules. Then redesign the system and apply it consistently.

## Operating contract

1. **Audit before editing.** Map the complete user-facing surface before changing the first screen.
2. **Review the whole product.** Shared navigation, tokens, components, layouts, and state patterns matter more than an isolated pretty screen.
3. **Preserve product meaning.** Do not change business logic, permissions, data semantics, or core workflows just for cosmetics. Separate UX problems from visual problems.
4. **Design before decoration.** Prioritize task hierarchy, information architecture, spacing rhythm, typography, layout, density, and interaction clarity before gradients, shadows, blur, or animation.
5. **Prefer system-level fixes.** Repeated visual drift should be fixed in tokens/components, not patched screen-by-screen.
6. **Use realistic states.** Inspect loading, empty, error, success, disabled, hover, focus, selected, validation, overflow, and permission states.
7. **Treat accessibility as polish.** Keyboard access, semantic controls, visible focus, contrast, text scaling/reflow, target size, and error recovery are part of production quality.
8. **Responsive means re-composition.** Do not just shrink desktop. Decide what reflows, collapses, disappears, becomes scrollable, or changes presentation at each size class.
9. **Avoid design-system cargo cults.** Existing libraries are implementation tools, not a reason to inherit their default visual identity.
10. **One source of truth.** New visual decisions should use reusable semantic tokens and shared components where the architecture allows it.

## Phase 0 — Establish the evidence boundary

Identify:

- framework/runtime and routing;
- styling system and component libraries;
- theme modes;
- token/theme files;
- shared shells/components;
- browser/emulator/screenshot capabilities;
- tests, Storybook, Figma exports, screenshots, and product requirements.

Prefer rendered evidence. If rendering is unavailable, inspect code/assets and mark visual claims as code-inferred. Never invent a visual observation.

## Phase 1 — Scan every screen

Find every user-facing route/screen, including important modals, drawers, sheets, auth, onboarding, loading, empty, error, and detail states.

Build an internal inventory:

| ID | Screen/Route | Type | User goal | Primary CTA | Density | Shared shell | States | Responsive risks |
|---|---|---|---|---|---|---|---|---|

Trace navigation so screens are judged in workflow context.

For each screen answer:

- What is the user trying to accomplish?
- What must they notice first?
- What is secondary?
- What can be progressively disclosed?
- What is the primary action?
- What is risky/destructive?
- What must persist while scrolling?

## Phase 2 — Detect vibe-coded signals

These are **signals, not automatic faults**. Investigate clusters and context.

### Generic visual signals

- Inter/system typography without a deliberate visual identity;
- Lucide/Heroicons used as unexamined defaults;
- generic blue/purple gradients;
- every surface inside a rounded card;
- identical radii everywhere;
- excessive pill controls/badges;
- blur/glass effects used as decoration;
- low-contrast gray-on-gray text;
- the same soft shadow on every surface;
- repeated oversized heading + muted subtitle patterns;
- nested card-within-card structures;
- decorative KPI cards that repeat information;
- generic dashboard grids;
- large empty areas on dense screens or cramped layouts on task screens.

### Structural signals

- every page follows the same title → subtitle → cards → table template;
- page titles are detached from the actual task;
- primary and secondary actions have equal emphasis;
- too many top-level navigation destinations;
- list rows look like cards instead of a scannable collection;
- forms mirror backend fields instead of user intent;
- arbitrary max-widths/breakpoints;
- inconsistent content edges and alignment;
- duplicated page shells with slightly different spacing;
- layout only works with short placeholder content.

### Interaction/state signals

- clickable-looking non-semantic elements;
- icon-only actions without accessible names;
- hover-only information;
- weak/missing focus;
- custom dialogs without robust focus management;
- destructive actions visually indistinguishable from safe actions;
- missing loading/empty/error/success/disabled/validation states;
- unclear required vs optional form fields;
- motion used to compensate for weak hierarchy.

### Implementation signals

- duplicated CSS values and near-identical variants;
- one-off styling for repeated components;
- ad-hoc variant conditionals;
- inline styles that drift;
- arbitrary values bypassing tokens;
- multiple icon packages;
- multiple button/input/card implementations;
- local colors instead of semantic variables;
- hardcoded dimensions that fail at other widths.

## Phase 3 — Reconstruct the design language

Infer or propose:

### Brand personality
Choose 3–5 specific words such as precise, calm, premium, utilitarian, editorial, technical, energetic, or welcoming. "Modern" alone is insufficient.

### Visual grammar
Define:

- typography family, roles, scale, and line-height;
- semantic color roles and neutral/background strategy;
- spacing scale;
- radius scale;
- border strategy;
- elevation/shadow strategy;
- icon family, size, and stroke conventions;
- container/max-width rules;
- grid/column rules;
- control heights;
- image treatment;
- motion/focus/selection/error/success language.

### Identity test
Ask: **If the logo and product name disappeared, would this still be distinguishable from 20 unrelated AI-generated apps?**

If not, define at least three differentiated visual or compositional signatures grounded in the product domain rather than decoration.

## Phase 4 — Score every screen

Score 0–5 for:

- hierarchy;
- layout/composition;
- spacing/alignment;
- typography;
- color/contrast;
- consistency;
- information density;
- interaction clarity;
- responsive/adaptive behavior;
- states/edge cases;
- accessibility;
- product distinctiveness.

Use this weighting:

- hierarchy 15%;
- layout 12%;
- spacing 10%;
- typography 10%;
- interaction 10%;
- consistency 10%;
- responsive 10%;
- accessibility 8%;
- states 5%;
- color/contrast 5%;
- density 3%;
- distinctiveness 2%.

Treat the result as a diagnostic, not an objective truth. Explain evidence behind every score below 4.

Severity:

- **P0** — blocks core task, accessibility, or usable interaction.
- **P1** — major hierarchy, navigation, responsive, or system problem.
- **P2** — noticeable quality/clarity problem.
- **P3** — refinement.

Prioritize:

`Task failure > Accessibility failure > Information hierarchy > Navigation/IA > Responsive breakage > System inconsistency > Density/spacing > Typography > Color/polish > Decoration`

## Phase 5 — Produce one global redesign direction

Before screen rewrites, produce:

1. What to stop doing.
2. What to keep because it is product-specific.
3. What to introduce.
4. 5–8 operational design principles.
5. Proposed design tokens.
6. Shared component changes.
7. Responsive rules.
8. Product identity strategy.

Do not choose a trend merely because it is popular. Make the design fit the product's users, tasks, domain, and information density.

## Phase 6 — Rewrite every screen

For each screen output:

### A. Screen role
One sentence describing the user's goal.

### B. Diagnosis
Prioritized problems tied to visible or code-backed evidence.

### C. New composition
Describe the screen from top to bottom: grouping, containment, alignment, hierarchy, and whitespace.

### D. Priority ladder
Label:

- primary information;
- secondary information;
- supporting information;
- primary action;
- secondary actions;
- destructive/risky action.

### E. Component changes
Identify reusable primitives and shared patterns.

### F. Visual changes
Specify exact direction for typography, spacing, surfaces, color roles, radii, borders, shadows, and iconography.

### G. Responsive behavior
For compact, medium, and large widths specify what reflows, collapses, disappears, becomes scrollable, stacks, or changes presentation.

### H. State matrix
Specify relevant loading, empty, error, success, disabled, selected, focus, validation, overflow, and permission states.

### I. Rewrite command
End with a concrete implementation instruction. Never end with "make it more modern/premium/clean."

**Bad:**
> Make this page feel more premium and modern.

**Good:**
> Replace four equal-weight metric cards with one primary metric strip plus a secondary comparison row. Use one semantic surface, a 12-column desktop grid, a 24px section rhythm, 16px compact gaps, and one accent reserved for positive deltas. Align the page title and primary action to the content column. Do not introduce gradients or new card types.

## Phase 7 — Rebuild the shared system before mass-editing screens

Inspect or create, only when evidenced by repetition:

### Tokens

Typography, semantic colors, spacing, control heights, radius, borders, elevation, motion, breakpoints/window classes, z-index.

### Shared primitives

AppShell/PageShell, page header, navigation, buttons, inputs, form fields, surfaces/cards, list rows, status/badges, tabs, tables/data grids, dialogs/drawers/sheets, popovers/tooltips, empty states, loading/skeletons, alerts/toasts, avatars/media, pagination, filters/search.

Avoid creating a giant component library before you understand the product.

## Phase 8 — Implement in controlled passes

1. **Foundation:** tokens, type, global surfaces, page container, navigation, core controls.
2. **Highest-impact screens:** fix 2–3 key screens first; they become reference standards.
3. **Shared patterns:** propagate corrected components/layouts to siblings.
4. **Real states:** finish loading/empty/error/disabled/focus/permission/overflow states.
5. **Responsive:** test compact, medium, and large layouts.
6. **Visual QA:** re-render, compare, and fix regressions before proceeding.

Do not accept "it compiles" as the visual definition of done.

## Visual QA

Check each changed screen for:

- shared content edges and alignment;
- vertical rhythm;
- title-to-content spacing;
- control height consistency;
- icon optical alignment;
- realistic text wrapping;
- long labels and numeric extremes;
- empty/loading/error/disabled/focus states;
- keyboard navigation;
- touch/pointer target size;
- contrast;
- zoom/text scaling;
- theme variants;
- reduced motion where applicable;
- responsive transitions;
- sticky/fixed elements obscuring content;
- consistency with already-refactored screens.

When screenshots can be captured, keep before/after evidence.

## Accessibility baseline

Use WCAG 2.2 for web projects unless the project requires more.

Verify at minimum:

- semantic controls and names/roles/values;
- keyboard access;
- visible and non-obscured focus;
- text and non-text contrast;
- resize/reflow;
- target size and spacing;
- meaningful headings and labels;
- error identification/recovery;
- non-text alternatives where relevant.

## Responsive/adaptive baseline

Treat responsive UI as a transformation system. For each major component define:

- minimum useful width;
- maximum useful width;
- intrinsic/flexible/fixed behavior;
- wrapping and overflow;
- collapse rules;
- navigation transformation;
- presentation transformation;
- priority-based hiding/revealing.

Use max-width constraints for readable content instead of stretching everything. Use panes/containers to preserve hierarchy. Do not use the same navigation pattern at every size without validating ergonomics and information architecture.

## Content realism

Test long names, large numbers, multi-line descriptions, missing images, empty datasets, validation errors, status variants, permissions, timestamps, and localized copy where relevant.

A design that only looks good with placeholder content is not fixed.

## Screenshot/reference handling

Treat screenshots as evidence of current output, not a complete specification. Identify viewport, hierarchy, repeated patterns, anomalies, likely responsive behavior, and what cannot be verified from pixels.

Treat visual references as principle sources, not clones. Extract hierarchy, spacing, composition, typography behavior, density, interaction patterns, surface treatment, and responsive strategy. Do not copy another product's brand identity unless explicitly requested.

## Output contract

Unless the user asks for another format, return:

1. Executive diagnosis.
2. Global score + top 10 issues.
3. Screen inventory.
4. Global design direction.
5. Design-token proposal.
6. Shared-component refactor plan.
7. Screen-by-screen redesign specifications.
8. Responsive/adaptive plan.
9. Accessibility + state matrix.
10. Implementation order.
11. Validation checklist.
12. Assumptions/unverified claims.

Every screen must end with:

**Rewrite command:** a concise implementation instruction another coding agent can execute without making unbounded aesthetic guesses.

## Guardrails

Do not:

- add decoration just to look premium;
- increase radius everywhere;
- create a new color for every component;
- create a component for every one-off situation;
- replace every card with flat layouts or vice versa without evidence;
- force a trend onto a product domain;
- remove useful information merely to create whitespace;
- hide important actions behind menus only for aesthetics;
- use tiny text to fit more content;
- make every control pill-shaped;
- use gradients as a substitute for brand identity;
- change semantics because a visual pattern looks cleaner;
- preserve a bad layout because it already exists;
- refactor working business logic unnecessarily during UI work.

## Definition of done

The interface is unvibecoded when:

- the product has a recognizable visual language;
- major screens share intentional tokens/primitives;
- hierarchy is clear;
- alignment and spacing are systematic;
- typography has deliberate roles;
- color has semantic purpose;
- component variants are controlled;
- responsive behavior is designed, not accidental;
- real states are covered;
- accessibility is production-grade;
- realistic content does not break layouts;
- one-off styling is reduced;
- future screens can be added without reinventing the visual system.

## Supporting resources

- [AUDIT-FRAMEWORK.md](references/AUDIT-FRAMEWORK.md) — detailed diagnostic lenses, screen heuristics, priorities, and three redesign strategies.
- [DESIGN-SYSTEM.md](references/DESIGN-SYSTEM.md) — token, typography, surface, icon, form, dense-data, responsive, and accessibility guidance.
- [REWRITE-TEMPLATES.md](references/REWRITE-TEMPLATES.md) — implementation-ready global/screen/component rewrite templates and vague-language converters.
- [SOURCES.md](references/SOURCES.md) — research basis and source links.
- `scripts/ui_signal_scan.py` — lightweight static scanner for common signals; heuristic only.
