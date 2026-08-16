# UnvibeCode Audit Framework

## 1. Diagnostic model

Use six lenses simultaneously:

1. **Product lens** — what is the user trying to accomplish?
2. **Composition lens** — what should dominate, support, or disappear?
3. **System lens** — what repeated rules make screens feel like one product?
4. **Interaction lens** — how does the interface behave in real states and inputs?
5. **Adaptation lens** — how does the composition transform across size classes?
6. **Implementation lens** — can the visual language be maintained without one-off code?

A screen can fail any one of these while looking attractive.

## 2. Evidence quality

Every observation should be labeled internally as one of:

- **Rendered evidence** — verified from a live browser/emulator render.
- **Screenshot evidence** — verified from supplied imagery.
- **Code evidence** — inferred from components/styles/routes.
- **Design inference** — a reasoned conclusion that still needs validation.

Do not present design inference as a measured fact.

## 3. Vibe-code pattern clusters

### Cluster A — Generic visual language

Typical cluster:
`Inter + rounded cards + muted gray surfaces + blue/purple accent + generic outline icons + soft shadows`.

Response: do not automatically replace each element. Ask what product-specific visual decision should replace the generic average.

### Cluster B — Cardification

Everything becomes a card. This creates nested boundaries and equal visual weight.

Response:
- retain containment where users need grouping;
- flatten secondary grouping when whitespace can communicate relationships;
- reserve strong surfaces for meaningful boundaries;
- avoid card-within-card-within-card hierarchy.

### Cluster C — Token drift

Symptoms:
- 14px in one component, 15px in another, 16px in another for the same semantic role;
- many near-identical radii;
- arbitrary spacing values;
- repeated hex values with no semantic names.

Response: consolidate into a semantic token system.

### Cluster D — Template inheritance

Every page is `title + subtitle + cards + table + CTA`, even when the user task differs.

Response: derive composition from the task first, then choose a layout pattern.

### Cluster E — Decoration as identity

The product uses gradients, blobs, glows, or glass panels to appear distinctive, but the underlying hierarchy remains generic.

Response: differentiate through composition, typography, density, control behavior, imagery, or brand-specific motifs before adding effects.

## 4. Screen-specific heuristics

### Dashboard

Ask:
- What decision should the dashboard enable?
- Which metric is genuinely primary?
- Are all metrics given equal visual weight?
- Are charts explanatory or decorative?
- Is there a clear next action?

Common rewrite: compress low-value KPI cards, strengthen primary metric, introduce meaningful groupings, reduce decorative chart noise.

### List/index

Ask:
- Is the row optimized for scanning?
- What fields are necessary to make a decision?
- Which metadata can be secondary?
- Are actions discoverable without visual clutter?

Common rewrite: use row anatomy rather than cards unless each item needs strong containment.

### Detail

Ask:
- Is identity/context obvious?
- Does the page have a clear task hierarchy?
- Are supporting details organized into meaningful sections?
- Which action persists?

Common rewrite: strong identity/header, one primary action, progressive disclosure for secondary information.

### Forms

Ask:
- Are fields ordered by user intent rather than backend schema?
- Are required/optional fields obvious?
- Can errors be corrected locally?
- Is there safe cancellation/recovery?

Common rewrite: group related tasks, reduce unnecessary borders, strengthen labels and help text, make the primary submit action unambiguous.

### Settings

Ask:
- Are preferences grouped by concept?
- Can the user understand consequences?
- Is navigation between settings sections predictable?
- Are dangerous settings separated?

Common rewrite: use a clear settings hierarchy with section navigation, concise descriptions, and contextual controls.

### Analytics/reporting

Ask:
- What question does each visualization answer?
- Can the user compare values without decoding decoration?
- Are units, ranges, and time periods explicit?
- Do tables provide an accessible alternative where necessary?

Common rewrite: prioritize decision-support over dashboard ornament.

## 5. Priority algorithm

When there are many issues, prioritize in this order:

`Task failure > Accessibility failure > Information hierarchy > Navigation/IA > Responsive breakage > System inconsistency > Density/spacing > Typography > Color/visual polish > Decorative refinement`

Do not spend an hour tuning shadows while the primary action is visually lost.

## 6. Three redesign strategies

### Strategy 1 — Surgical de-vibing

Use when the existing product is structurally sound.

Change:
- typography;
- token consistency;
- surface/radius strategy;
- hierarchy;
- component polish;
- state completeness.

Keep most structure and business logic.

### Strategy 2 — System reconstruction

Use when the code contains duplicated UI patterns and visual drift.

Change:
- token layer;
- shared components;
- page shell;
- navigation;
- repeated layouts;
- states.

Then recompose screens using the system.

### Strategy 3 — Workflow reconstruction

Use when the interface looks polished but the task flow is fundamentally wrong.

Change:
- information architecture;
- navigation hierarchy;
- page composition;
- progressive disclosure;
- task-specific states.

Do not hide this category under cosmetic language.

## 7. Example diagnosis → rewrite

### Example A — Generic dashboard

**Diagnosis:** four equal KPI cards, two decorative charts, oversized greeting, and no clear operational next step.

**Rewrite:** lead with the primary operational metric and the action it informs; group supporting metrics by decision; use charts only where trend/context changes a decision; move recent activity into a compact scan-friendly section.

### Example B — Generic CRUD list

**Diagnosis:** every item is a rounded white card with four lines of metadata and a three-dot menu.

**Rewrite:** convert to a dense row/table pattern with consistent columns, strong primary label, secondary metadata, visible status, and row-level actions. Use cards only for contexts where items are independently actionable or visually distinct.

### Example C — Generic settings page

**Diagnosis:** every setting is an isolated card, causing excessive vertical scanning.

**Rewrite:** create a single settings content column with section headers, short explanations, clear control alignment, grouped dangerous actions, and an anchored save/discard model only when unsaved changes are real.
