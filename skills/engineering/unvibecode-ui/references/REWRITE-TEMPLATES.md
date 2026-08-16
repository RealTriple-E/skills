# Rewrite Templates

## Global redesign brief

```text
PRODUCT:
[product name]

PRIMARY USERS:
[user roles]

PRIMARY JOBS:
[top tasks]

CURRENT PROBLEMS:
[highest-impact findings]

VISUAL IDENTITY:
[3–5 product-specific adjectives]

DESIGN PRINCIPLES:
1.
2.
3.
4.
5.

TOKEN SYSTEM:
Typography:
Colors:
Spacing:
Radii:
Borders:
Elevation:
Controls:
Motion:

COMPONENT RULES:
[shared primitives and variants]

RESPONSIVE RULES:
Compact:
Medium:
Large:

DO NOT:
[anti-patterns to avoid]
```

## Screen rewrite

```text
SCREEN:
[route/name]

USER GOAL:
[one sentence]

CURRENT PROBLEMS:
1.
2.
3.

PRIMARY INFORMATION:
[...] 
SECONDARY INFORMATION:
[...]
SUPPORTING INFORMATION:
[...]
PRIMARY ACTION:
[...]
SECONDARY ACTIONS:
[...]
RISKY/DESTRUCTIVE ACTION:
[...]

NEW COMPOSITION:
1. [top-level shell]
2. [header/task context]
3. [primary content]
4. [secondary content]
5. [supporting content]

COMPONENTS:
[shared primitives]

VISUAL RULES:
Typography:
Spacing:
Surfaces:
Color:
Icons:
Borders:
Elevation:

RESPONSIVE:
Compact:
Medium:
Large:

STATES:
Loading:
Empty:
Error:
Success:
Disabled:
Focus:
Selected:
Overflow:

REWRITE COMMAND:
[implementation-ready instruction]
```

## Component rewrite command

```text
Keep the component's behavior and API unless there is a clear UX defect.
Replace ad-hoc styling with the shared semantic tokens.
Use the product's canonical type scale, spacing scale, radius scale, and surface strategy.
Preserve semantic hierarchy and accessible states.
Do not introduce a new visual pattern when an existing component can represent the state.
Add responsive behavior according to the parent screen's layout rules.
Test realistic content before accepting the component.
```

## Anti-vague language converter

Replace:

- "make it modern" → "define the exact hierarchy, density, typography, and surface changes";
- "make it premium" → "specify material, typography, spacing, and product personality";
- "make it clean" → "remove redundant visual boundaries and clarify grouping";
- "make it professional" → "define hierarchy, alignment, consistency, content realism, and state completeness";
- "make it responsive" → "define component and navigation transformations by size class";
- "make it less AI-looking" → "remove generic pattern clusters and introduce product-specific composition/typography/interaction decisions".
