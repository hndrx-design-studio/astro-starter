# CSS Variables Reference

This document provides a complete reference of all CSS custom properties (variables) used in the design system, aligned with the **Relume Figma Kit (v. 3.7)** for seamless Figma-to-code workflow.

## Figma Token Integration

The design system tokens are derived from the Relume Figma Kit exports located in `/figma-style-tokens/`:

| Token File | Purpose |
|------------|---------|
| `Primitives-tokens.json` | Raw color values and opacity variants |
| `Color-Schemes-tokens.json` | Semantic color assignments (Text, Background, Border, etc.) |
| `Typography-Desktop-tokens.json` | Font sizes for desktop (≥768px) |
| `Typography-Mobile-tokens.json` | Font sizes for mobile (<768px) |
| `Spacing-and-Sizing-Desktop-tokens.json` | Container, padding, max-width for desktop |
| `Spacing-and-Sizing-Mobile-tokens.json` | Container, padding, max-width for mobile |
| `UIStyles-tokens.json` | Border radius and stroke widths |

## Naming Convention

Variables follow Relume's naming patterns with CSS best practices:

```
--{category}-{property}-{variant}
```

### Examples

```css
--color-neutral-darkest     /* Primitive: darkest neutral color */
--color-text                /* Semantic: main text color (from Color Scheme) */
--text-size-h1              /* Typography: heading 1 size */
--padding-section-large     /* Spacing: large section padding */
--container-large           /* Layout: large container max-width */
```

---

## Design Tokens

### Color Primitives (from Figma: Primitives-tokens.json)

#### Neutral Scale

| Variable | Hex | Description |
|----------|-----|-------------|
| `--color-white` | `#FFFFFF` | Pure white |
| `--color-neutral-lightest` | `#EEEEEE` | Lightest neutral |
| `--color-neutral-lighter` | `#CCCCCC` | Lighter neutral |
| `--color-neutral-light` | `#AAAAAA` | Light neutral |
| `--color-neutral` | `#666666` | Base neutral |
| `--color-neutral-dark` | `#444444` | Dark neutral |
| `--color-neutral-darker` | `#222222` | Darker neutral |
| `--color-neutral-darkest` | `#000000` | Darkest neutral (black) |

#### Opacity Variants - White

| Variable | Value | Description |
|----------|-------|-------------|
| `--color-transparent` | `rgba(255, 255, 255, 0)` | Fully transparent |
| `--color-white-5` | `rgba(255, 255, 255, 0.05)` | 5% white |
| `--color-white-10` | `rgba(255, 255, 255, 0.10)` | 10% white |
| `--color-white-15` | `rgba(255, 255, 255, 0.15)` | 15% white |
| `--color-white-20` | `rgba(255, 255, 255, 0.20)` | 20% white |
| `--color-white-30` | `rgba(255, 255, 255, 0.30)` | 30% white |
| `--color-white-40` | `rgba(255, 255, 255, 0.40)` | 40% white |
| `--color-white-50` | `rgba(255, 255, 255, 0.50)` | 50% white |
| `--color-white-60` | `rgba(255, 255, 255, 0.60)` | 60% white |

#### Opacity Variants - Black

| Variable | Value | Description |
|----------|-------|-------------|
| `--color-black-5` | `rgba(0, 0, 0, 0.05)` | 5% black |
| `--color-black-10` | `rgba(0, 0, 0, 0.10)` | 10% black |
| `--color-black-15` | `rgba(0, 0, 0, 0.15)` | 15% black |
| `--color-black-20` | `rgba(0, 0, 0, 0.20)` | 20% black |
| `--color-black-30` | `rgba(0, 0, 0, 0.30)` | 30% black |
| `--color-black-40` | `rgba(0, 0, 0, 0.40)` | 40% black |
| `--color-black-50` | `rgba(0, 0, 0, 0.50)` | 50% black |
| `--color-black-60` | `rgba(0, 0, 0, 0.60)` | 60% black |

### Color Scheme (from Figma: Color-Schemes-tokens.json)

These semantic tokens reference the primitives and define the color scheme for the site.

| Variable | Default | Figma Name | Description |
|----------|---------|------------|-------------|
| `--color-text` | `--color-neutral-darkest` | Text | Primary text color |
| `--color-foreground` | `--color-white` | Foreground | Icons, UI elements |
| `--color-background` | `--color-white` | Background | Page background |
| `--color-border` | `--color-neutral-darkest` | Border | Primary border color |
| `--color-accent` | `--color-neutral-darkest` | Accent | Accent/brand color |

#### Extended Semantic Colors

| Variable | Default | Description |
|----------|---------|-------------|
| `--color-text-primary` | `--color-neutral-darkest` | Main text |
| `--color-text-secondary` | `--color-neutral` | Secondary text |
| `--color-text-tertiary` | `--color-neutral-light` | Muted text |
| `--color-text-inverse` | `--color-white` | Text on dark backgrounds |
| `--color-text-link` | `--color-neutral-darkest` | Link color |
| `--color-text-link-hover` | `--color-neutral-dark` | Link hover |
| `--color-bg-primary` | `--color-white` | Main background |
| `--color-bg-secondary` | `--color-neutral-lightest` | Secondary background |
| `--color-bg-tertiary` | `--color-neutral-lighter` | Tertiary background |
| `--color-bg-inverse` | `--color-neutral-darkest` | Dark background |
| `--color-border-default` | `--color-neutral-lighter` | Default borders |
| `--color-border-strong` | `--color-neutral-light` | Strong borders |
| `--color-border-focus` | `--color-neutral-darkest` | Focus states |

#### Status Colors (Extended)

| Variable | Value | Description |
|----------|-------|-------------|
| `--color-success` | `#22C55E` | Success base |
| `--color-success-light` | `#DCFCE7` | Success background |
| `--color-success-dark` | `#16A34A` | Success dark |
| `--color-warning` | `#EAB308` | Warning base |
| `--color-warning-light` | `#FEF9C3` | Warning background |
| `--color-warning-dark` | `#CA8A04` | Warning dark |
| `--color-error` | `#EF4444` | Error base |
| `--color-error-light` | `#FEE2E2` | Error background |
| `--color-error-dark` | `#DC2626` | Error dark |

---

### Typography (from Figma: Typography tokens)

Typography variables are responsive - they automatically adjust on mobile via CSS media queries.

#### Font Families

| Variable | Default |
|----------|---------|
| `--font-family-sans` | `system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif` |
| `--font-family-serif` | `Georgia, Cambria, 'Times New Roman', Times, serif` |
| `--font-family-mono` | `'SF Mono', SFMono-Regular, Consolas, 'Liberation Mono', Menlo, monospace` |

#### Text Sizes (Responsive)

| Variable | Desktop | Mobile | Figma Name |
|----------|---------|--------|------------|
| `--text-size-h1` | `3.5rem (56px)` | `2.5rem (40px)` | Heading 1 |
| `--text-size-h2` | `3rem (48px)` | `2.25rem (36px)` | Heading 2 |
| `--text-size-h3` | `2.5rem (40px)` | `2rem (32px)` | Heading 3 |
| `--text-size-h4` | `2rem (32px)` | `1.5rem (24px)` | Heading 4 |
| `--text-size-h5` | `1.5rem (24px)` | `1.25rem (20px)` | Heading 5 |
| `--text-size-h6` | `1.25rem (20px)` | `1.125rem (18px)` | Heading 6 |
| `--text-size-large` | `1.25rem (20px)` | `1.125rem (18px)` | Text Large |
| `--text-size-medium` | `1.125rem (18px)` | `1rem (16px)` | Text Medium |
| `--text-size-regular` | `1rem (16px)` | `1rem (16px)` | Text Regular |
| `--text-size-small` | `0.875rem (14px)` | `0.875rem (14px)` | Text Small |
| `--text-size-tiny` | `0.75rem (12px)` | `0.75rem (12px)` | Text Tiny |

#### Legacy Font Size Aliases

For backwards compatibility, these aliases map to the new Relume tokens:

| Variable | Maps To |
|----------|---------|
| `--font-size-xs` | `--text-size-tiny` |
| `--font-size-sm` | `--text-size-small` |
| `--font-size-base` | `--text-size-regular` |
| `--font-size-lg` | `--text-size-medium` |
| `--font-size-xl` | `--text-size-large` |
| `--font-size-2xl` | `--text-size-h5` |
| `--font-size-3xl` | `--text-size-h4` |
| `--font-size-4xl` | `--text-size-h3` |
| `--font-size-5xl` | `--text-size-h2` |
| `--font-size-6xl` | `--text-size-h1` |

#### Font Weights

| Variable | Value |
|----------|-------|
| `--font-weight-light` | `300` |
| `--font-weight-normal` | `400` |
| `--font-weight-medium` | `500` |
| `--font-weight-semibold` | `600` |
| `--font-weight-bold` | `700` |

#### Line Heights

| Variable | Value |
|----------|-------|
| `--line-height-none` | `1` |
| `--line-height-tight` | `1.2` |
| `--line-height-snug` | `1.3` |
| `--line-height-normal` | `1.5` |
| `--line-height-relaxed` | `1.6` |
| `--line-height-loose` | `2` |

#### Letter Spacing

| Variable | Value |
|----------|-------|
| `--letter-spacing-tighter` | `-0.05em` |
| `--letter-spacing-tight` | `-0.025em` |
| `--letter-spacing-normal` | `0` |
| `--letter-spacing-wide` | `0.025em` |
| `--letter-spacing-wider` | `0.05em` |

---

### Spacing & Layout (from Figma: Spacing-and-Sizing tokens)

#### Base Spacing Scale

| Variable | Value | Pixels |
|----------|-------|--------|
| `--space-0` | `0` | 0px |
| `--space-1` | `0.25rem` | 4px |
| `--space-2` | `0.5rem` | 8px |
| `--space-3` | `0.75rem` | 12px |
| `--space-4` | `1rem` | 16px |
| `--space-5` | `1.25rem` | 20px |
| `--space-6` | `1.5rem` | 24px |
| `--space-8` | `2rem` | 32px |
| `--space-10` | `2.5rem` | 40px |
| `--space-12` | `3rem` | 48px |
| `--space-16` | `4rem` | 64px |
| `--space-20` | `5rem` | 80px |
| `--space-24` | `6rem` | 96px |
| `--space-28` | `7rem` | 112px |
| `--space-32` | `8rem` | 128px |

#### Page Padding (Responsive)

| Variable | Desktop | Mobile | Figma Name |
|----------|---------|--------|------------|
| `--padding-global` | `4rem (64px)` | `1.25rem (20px)` | padding-global |

#### Section Padding (Responsive)

| Variable | Desktop | Mobile | Figma Name |
|----------|---------|--------|------------|
| `--padding-section-large` | `7rem (112px)` | `4rem (64px)` | padding-section-large |
| `--padding-section-medium` | `5rem (80px)` | `3rem (48px)` | padding-section-medium |
| `--padding-section-small` | `3rem (48px)` | `2rem (32px)` | padding-section-small |

#### Container Widths (from Figma)

| Variable | Value | Figma Name |
|----------|-------|------------|
| `--container-large` | `80rem (1280px)` | container-large |
| `--container-medium` | `64rem (1024px)` | container-medium |
| `--container-small` | `48rem (768px)` | container-small |

#### Max Width Scale (from Figma)

| Variable | Value | Figma Name |
|----------|-------|------------|
| `--max-width-xxlarge` | `80rem (1280px)` | max-width-xxlarge |
| `--max-width-xlarge` | `64rem (1024px)` | max-width-xlarge |
| `--max-width-large` | `48rem (768px)` | max-width-large |
| `--max-width-medium` | `35rem (560px)` | max-width-medium |
| `--max-width-small` | `30rem (480px)` | max-width-small |
| `--max-width-xsmall` | `25rem (400px)` | max-width-xsmall |
| `--max-width-xxsmall` | `20rem (320px)` | max-width-xxsmall |

---

### UI Styles (from Figma: UIStyles-tokens.json)

#### Border Radius

| Variable | Value | Figma Name |
|----------|-------|------------|
| `--radius-small` | `0` | Small |
| `--radius-medium` | `0` | Medium |
| `--radius-large` | `0` | Large |

> **Note:** Relume defaults to 0 for unstyled components. Override these for rounded designs.

#### Extended Radius (for customization)

| Variable | Value | Pixels |
|----------|-------|--------|
| `--radius-none` | `0` | 0px |
| `--radius-sm` | `0.25rem` | 4px |
| `--radius-md` | `0.375rem` | 6px |
| `--radius-lg` | `0.5rem` | 8px |
| `--radius-xl` | `0.75rem` | 12px |
| `--radius-2xl` | `1rem` | 16px |
| `--radius-3xl` | `1.5rem` | 24px |
| `--radius-full` | `9999px` | Fully rounded |

#### Stroke Widths

| Variable | Value | Figma Name |
|----------|-------|------------|
| `--stroke-border-width` | `1px` | Border Width |
| `--stroke-divider-width` | `1px` | Divider Width |

---

### Shadows

| Variable | Value |
|----------|-------|
| `--shadow-xs` | `0 1px 2px 0 var(--color-black-5)` |
| `--shadow-sm` | `0 1px 3px 0 var(--color-black-10), 0 1px 2px -1px var(--color-black-10)` |
| `--shadow-md` | `0 4px 6px -1px var(--color-black-10), 0 2px 4px -2px var(--color-black-10)` |
| `--shadow-lg` | `0 10px 15px -3px var(--color-black-10), 0 4px 6px -4px var(--color-black-10)` |
| `--shadow-xl` | `0 20px 25px -5px var(--color-black-10), 0 8px 10px -6px var(--color-black-10)` |
| `--shadow-2xl` | `0 25px 50px -12px var(--color-black-30)` |
| `--shadow-inner` | `inset 0 2px 4px 0 var(--color-black-5)` |
| `--shadow-none` | `0 0 #0000` |

---

### Transitions

| Variable | Value |
|----------|-------|
| `--duration-instant` | `0ms` |
| `--duration-fast` | `100ms` |
| `--duration-normal` | `200ms` |
| `--duration-slow` | `300ms` |
| `--duration-slower` | `500ms` |
| `--ease-linear` | `linear` |
| `--ease-in` | `cubic-bezier(0.4, 0, 1, 1)` |
| `--ease-out` | `cubic-bezier(0, 0, 0.2, 1)` |
| `--ease-in-out` | `cubic-bezier(0.4, 0, 0.2, 1)` |
| `--transition-fast` | `100ms ease-in-out` |
| `--transition-normal` | `200ms ease-in-out` |
| `--transition-slow` | `300ms ease-in-out` |

---

### Z-Index Scale

| Variable | Value | Use Case |
|----------|-------|----------|
| `--z-dropdown` | `1000` | Dropdown menus |
| `--z-sticky` | `1020` | Sticky headers |
| `--z-fixed` | `1030` | Fixed elements |
| `--z-modal-backdrop` | `1040` | Modal overlay |
| `--z-modal` | `1050` | Modal dialogs |
| `--z-popover` | `1060` | Popovers |
| `--z-tooltip` | `1070` | Tooltips |

---

## Typography Classes

CSS classes that match Relume Figma component naming:

### Headings

| Class | Size Variable |
|-------|---------------|
| `.heading-1`, `h1` | `--text-size-h1` |
| `.heading-2`, `h2` | `--text-size-h2` |
| `.heading-3`, `h3` | `--text-size-h3` |
| `.heading-4`, `h4` | `--text-size-h4` |
| `.heading-5`, `h5` | `--text-size-h5` |
| `.heading-6`, `h6` | `--text-size-h6` |

### Body Text

| Class | Size Variable |
|-------|---------------|
| `.text-large` | `--text-size-large` |
| `.text-medium` | `--text-size-medium` |
| `.text-regular` | `--text-size-regular` |
| `.text-small` | `--text-size-small` |
| `.text-tiny` | `--text-size-tiny` |

---

## Layout Classes

### Containers

| Class | Max Width |
|-------|-----------|
| `.container` | `--container-large` (1280px) |
| `.container-large` | `--container-large` (1280px) |
| `.container-medium` | `--container-medium` (1024px) |
| `.container-small` | `--container-small` (768px) |
| `.container-full` | none |

### Max Width Utilities

| Class | Max Width |
|-------|-----------|
| `.max-width-xxlarge` | 1280px |
| `.max-width-xlarge` | 1024px |
| `.max-width-large` | 768px |
| `.max-width-medium` | 560px |
| `.max-width-small` | 480px |
| `.max-width-xsmall` | 400px |
| `.max-width-xxsmall` | 320px |

### Section Padding

| Class | Padding |
|-------|---------|
| `.section`, `.section-large` | `--padding-section-large` |
| `.section-medium` | `--padding-section-medium` |
| `.section-small` | `--padding-section-small` |
| `.padding-global` | `--padding-global` (horizontal) |

---

## Customization

### Overriding Tokens

To customize the design system for your brand, override the tokens in your CSS:

```css
:root {
  /* Custom brand colors */
  --color-accent: #3B82F6;
  --color-primary: #3B82F6;
  
  /* Custom border radius (make things rounded) */
  --radius-small: 4px;
  --radius-medium: 8px;
  --radius-large: 12px;
  
  /* Custom fonts */
  --font-family-sans: 'Inter', system-ui, sans-serif;
}
```

### Dark Mode

Enable dark mode by uncommenting the dark mode section in `tokens.css` or creating a custom theme:

```css
[data-theme="dark"] {
  --color-text: var(--color-white);
  --color-background: var(--color-neutral-darkest);
  --color-border: var(--color-white);
  /* ... */
}
```

---

## Component Variables

Components use their own scoped variables that reference design tokens. This allows component-specific customization while maintaining system consistency.

### Button (`--btn-*`)

| Variable | Fallback | Description |
|----------|----------|-------------|
| `--btn-font-family` | `--font-family-sans` | Font family |
| `--btn-font-weight` | `--font-weight-medium` | Font weight |
| `--btn-border-radius` | `--radius-medium` | Border radius |
| `--btn-border-width` | `--stroke-border-width` | Border width |
| `--btn-focus-ring-color` | `--color-border-focus` | Focus ring |

### Input (`--input-*`)

| Variable | Fallback |
|----------|----------|
| `--input-border-radius` | `--radius-medium` |
| `--input-border-width` | `--stroke-border-width` |
| `--input-border-color` | `--color-border-default` |
| `--input-focus-border-color` | `--color-border-focus` |

### Card (`--card-*`)

| Variable | Fallback |
|----------|----------|
| `--card-border-radius` | `--radius-large` |
| `--card-border-width` | `--stroke-border-width` |
| `--card-border-color` | `--color-border-default` |
| `--card-padding` | `--space-6` |

### Section (`--section-*`)

| Variable | Fallback |
|----------|----------|
| `--section-padding-y` | `--padding-section-large` |
| `--section-bg-default` | `--color-bg-primary` |
| `--section-bg-muted` | `--color-bg-secondary` |
