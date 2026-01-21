# Contributing Guide

Thank you for your interest in contributing to the Astro Starter with Vanilla CSS Design System. This guide will help you understand how to add new components and maintain consistency with the existing design system.

## Table of Contents

- [Project Philosophy](#project-philosophy)
- [Adding New Components](#adding-new-components)
- [CSS Variable Guidelines](#css-variable-guidelines)
- [Component Checklist](#component-checklist)
- [File Organization](#file-organization)
- [Documentation](#documentation)

---

## Project Philosophy

### Core Principles

1. **Unstyled by Default** - Components should be functional without being opinionated about visual design. All styling should be easily overridable.

2. **CSS Variables First** - Every visual property should be controlled by a CSS custom property with a sensible fallback to design tokens.

3. **No Dependencies** - Components should only depend on Astro. No JavaScript frameworks, CSS frameworks, or runtime dependencies.

4. **Accessibility** - All components must be accessible. Use semantic HTML, proper ARIA attributes, and visible focus states.

5. **Composition Over Configuration** - Prefer slots and composition patterns over complex prop APIs.

---

## Adding New Components

### 1. Determine the Atomic Level

| Level | Description | Examples |
|-------|-------------|----------|
| **Atoms** | Smallest, indivisible components | Button, Input, Badge, Icon |
| **Molecules** | Simple combinations of atoms | Card, FormField, NavLink |
| **Organisms** | Complex UI sections | Header, Footer, HeroSection |
| **Templates** | Page-level layouts | BaseLayout, BlogLayout |

### 2. Create the Component File

Create a new `.astro` file in the appropriate folder:

```
src/components/{level}/{ComponentName}.astro
```

### 3. Component Structure

Follow this template:

```astro
---
/**
 * ComponentName Component ({Level})
 *
 * Brief description of what the component does.
 *
 * @example
 * <ComponentName prop="value">Content</ComponentName>
 *
 * @customization
 * Override these CSS variables to customize:
 * --component-property-name
 */

interface Props {
  /** Description of the prop */
  propName?: 'option1' | 'option2';
  /** Allow custom classes */
  class?: string;
  /** Catch-all for HTML attributes */
  [key: string]: any;
}

const {
  propName = 'option1',
  class: className = '',
  ...rest
} = Astro.props;

// Build class list
const classes = [
  'component',
  `component--${propName}`,
  className,
].filter(Boolean).join(' ');
---

<element class={classes} {...rest}>
  <slot />
</element>

<style>
  .component {
    /* Use CSS variables with fallbacks */
    property: var(--component-property, var(--design-token));
  }

  .component--option1 {
    /* Variant styles */
  }

  .component--option2 {
    /* Variant styles */
  }
</style>
```

### 4. Export from Index

Add the export to the barrel file:

```typescript
// src/components/{level}/index.ts
export { default as ComponentName } from './ComponentName.astro';
```

### 5. Add to Style Guide

Add a section to `src/pages/style-guide.astro` demonstrating all component variants.

---

## CSS Variable Guidelines

### Naming Convention

```
--{component}-{property}-{variant}-{state}
```

Examples:
- `--btn-bg` - Button background
- `--btn-primary-bg` - Primary button background
- `--btn-primary-bg-hover` - Primary button hover background
- `--input-focus-ring-color` - Input focus ring color

### Required Patterns

#### 1. Always Use Fallbacks

```css
/* Good */
background: var(--btn-bg, var(--color-primary-600));

/* Bad - no fallback */
background: var(--btn-bg);
```

#### 2. Reference Design Tokens

```css
/* Good - references token */
padding: var(--btn-padding, var(--space-4));

/* Acceptable - hardcoded reasonable default */
padding: var(--btn-padding, 1rem);

/* Bad - magic number without context */
padding: var(--btn-padding, 16px);
```

#### 3. Namespace All Variables

```css
/* Good - namespaced to component */
--card-border-radius: var(--radius-lg);

/* Bad - generic name could conflict */
--border-radius: var(--radius-lg);
```

### Variable Categories

For each component, consider these categories:

| Category | Examples |
|----------|----------|
| **Layout** | padding, margin, gap, width, height |
| **Typography** | font-family, font-size, font-weight, line-height |
| **Colors** | background, color, border-color |
| **Borders** | border-width, border-radius |
| **Effects** | box-shadow, opacity |
| **States** | hover, focus, active, disabled |
| **Transitions** | transition-duration, transition-timing |

---

## Component Checklist

Before submitting a new component, verify:

### Structure
- [ ] Component is in the correct atomic level folder
- [ ] Uses TypeScript interface for props
- [ ] Has JSDoc comments with description and examples
- [ ] Lists customizable CSS variables in comments
- [ ] Exports from the barrel index file

### Props
- [ ] Accepts `class` prop for custom styling
- [ ] Uses rest props (`...rest`) for HTML attributes
- [ ] Has sensible defaults for optional props
- [ ] Props are properly typed (no `any` types)

### CSS
- [ ] All visual properties use CSS variables
- [ ] Variables have fallbacks to design tokens
- [ ] Variables are properly namespaced
- [ ] Uses BEM-like naming (component, component--variant, component__element)
- [ ] Styles are scoped (Astro's default behavior)

### Accessibility
- [ ] Uses semantic HTML elements
- [ ] Has visible focus states (`:focus-visible`)
- [ ] Includes ARIA attributes where needed
- [ ] Supports keyboard navigation
- [ ] Has sufficient color contrast

### Documentation
- [ ] Added to style guide page
- [ ] Shows all variants and states
- [ ] Includes code examples

---

## File Organization

### Component Files

```
src/components/
├── atoms/
│   ├── Button.astro       # Component file
│   ├── Input.astro
│   ├── Badge.astro
│   ├── Text.astro
│   └── index.ts           # Barrel export
├── molecules/
│   ├── Card.astro
│   ├── FormField.astro
│   ├── NavLink.astro
│   └── index.ts
├── organisms/
│   ├── Header.astro
│   ├── Footer.astro
│   ├── Section.astro
│   └── index.ts
└── templates/
    ├── BaseLayout.astro
    └── index.ts
```

### Style Files

```
src/styles/
├── design-system/
│   ├── tokens.css         # Design tokens (variables)
│   ├── typography.css     # Text styles
│   ├── spacing.css        # Spacing utilities
│   └── layout.css         # Layout utilities
├── base/
│   ├── reset.css          # CSS reset
│   └── global.css         # Global element styles
└── main.css               # Entry point
```

---

## Documentation

### Component Documentation

Each component should have:

1. **JSDoc header** in the component file:
   ```astro
   ---
   /**
    * Button Component (Atom)
    *
    * A flexible button with multiple variants and sizes.
    *
    * @example
    * <Button variant="primary">Click me</Button>
    *
    * @customization
    * --btn-border-radius, --btn-primary-bg, etc.
    */
   ---
   ```

2. **Style guide section** showing:
   - All variants
   - All sizes
   - All states (hover, focus, disabled)
   - Common use cases

### CSS Variables Documentation

Add new variables to `docs/CSS-VARIABLES.md` with:
- Variable name
- Default/fallback value
- Description of what it controls

---

## Common Patterns

### Variant Props

```astro
---
interface Props {
  variant?: 'primary' | 'secondary' | 'ghost';
}

const { variant = 'primary' } = Astro.props;
---

<button class={`btn btn--${variant}`}>
  <slot />
</button>
```

### Size Props

```astro
---
interface Props {
  size?: 'sm' | 'md' | 'lg';
}

const { size = 'md' } = Astro.props;
---

<div class={`component component--${size}`}>
  <slot />
</div>

<style>
  .component--sm {
    padding: var(--component-padding-sm, var(--space-2));
    font-size: var(--component-font-size-sm, var(--font-size-sm));
  }
  /* etc. */
</style>
```

### Polymorphic Components

```astro
---
interface Props {
  as?: 'button' | 'a';
  href?: string;
}

const { as: Element = 'button', href } = Astro.props;
---

{Element === 'a' ? (
  <a class="btn" href={href}><slot /></a>
) : (
  <button class="btn"><slot /></button>
)}
```

### Conditional Slots

```astro
---
const hasHeader = Astro.slots.has('header');
const hasFooter = Astro.slots.has('footer');
---

<div class="card">
  {hasHeader && (
    <div class="card__header">
      <slot name="header" />
    </div>
  )}

  <div class="card__body">
    <slot />
  </div>

  {hasFooter && (
    <div class="card__footer">
      <slot name="footer" />
    </div>
  )}
</div>
```

---

## Questions?

If you're unsure about anything, look at existing components for patterns to follow. The Button and Card components are good references for atoms and molecules respectively.
