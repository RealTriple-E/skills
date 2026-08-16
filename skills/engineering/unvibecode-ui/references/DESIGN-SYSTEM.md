# Design System Reconstruction Guide

## 1. Token hierarchy

Use semantic tokens rather than component-specific values.

Example:

```css
:root {
  --font-sans: ...;
  --font-display: ...;

  --text-strong: ...;
  --text-default: ...;
  --text-muted: ...;
  --text-inverse: ...;

  --surface-page: ...;
  --surface-raised: ...;
  --surface-subtle: ...;
  --surface-inverse: ...;

  --border-default: ...;
  --border-strong: ...;

  --accent: ...;
  --success: ...;
  --warning: ...;
  --danger: ...;

  --space-1: ...;
  --space-2: ...;
  --space-3: ...;
  --space-4: ...;
  --space-5: ...;
  --space-6: ...;

  --radius-sm: ...;
  --radius-md: ...;
  --radius-lg: ...;

  --control-sm: ...;
  --control-md: ...;
  --control-lg: ...;
}
```

The exact values are product-specific. The key is having a small, coherent vocabulary and assigning semantic meaning to it.

## 2. Typography

Give each role a job:

- display/marketing;
- page title;
- section heading;
- body;
- supporting text;
- metadata;
- label;
- data/number;
- code/monospace when needed.

Do not create a separate font size for every screen.

Minimize typeface count. Ensure hierarchy survives text scaling and realistic content lengths.

## 3. Spacing

Build a rhythm. Related items should usually have a smaller gap than unrelated sections.

Avoid arbitrary sequences such as 13px, 19px, 27px, 31px unless there is a reason. Prefer a small spacing vocabulary and compose with it.

## 4. Surface strategy

Decide when a surface is:

- page background;
- raised content;
- interactive control;
- selected/active;
- overlay;
- warning/danger.

Do not use the same shadow/radius treatment for every surface.

## 5. Icon strategy

Choose one primary icon family where practical. Define:

- stroke width;
- optical size;
- default size;
- text alignment;
- icon-only button behavior;
- filled vs outline usage.

Do not use icons as decoration when text already communicates the same idea and the icon adds noise.

## 6. Buttons

Define a small set of semantic variants:

- primary;
- secondary;
- tertiary/ghost;
- destructive;
- icon-only;
- loading/disabled.

The primary button should not simply be the most saturated object on every screen. Its emphasis should reflect task priority.

## 7. Forms

Define one field anatomy:

`label → optional description → control → validation/help`

Keep field labels, control heights, error behavior, and focus behavior consistent.

## 8. Data-dense interfaces

Use hierarchy rather than giant cards. Consider:

- rows;
- tables;
- grouped sections;
- density modes;
- inline status;
- sticky headers only where useful;
- progressive disclosure.

Dense does not mean cramped; it means information is prioritized and organized.

## 9. Responsive system

Do not make every component fluid in the same way.

For each component classify dimensions as:

- fixed where ergonomically necessary;
- intrinsic to content;
- constrained by max width;
- flexible within a grid;
- replaced by another presentation at a breakpoint.

## 10. Accessibility system

Each component should define:

- semantic element;
- accessible name;
- keyboard behavior;
- focus-visible behavior;
- disabled state;
- error state;
- selected/pressed state;
- minimum usable target area;
- reduced-motion behavior if animated.

Use a proven accessible primitive layer when appropriate rather than repeatedly implementing complex interaction semantics from scratch.
