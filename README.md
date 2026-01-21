# Astro Starter with Vanilla CSS Design System

A minimal, unstyled Astro starter template featuring an atomic design component library and a vanilla CSS design system. Built for developers who want full control over their styling without framework dependencies.

## Features

- **Atomic Design Architecture** - Components organized into atoms, molecules, organisms, and templates
- **Vanilla CSS Design System** - No Tailwind, no CSS-in-JS, just pure CSS with custom properties
- **Fully Customizable** - Override any design token or component style via CSS variables
- **Zero Runtime Dependencies** - Only Astro as a dependency
- **Copy-Paste Components** - Each component is self-contained and documented
- **Built-in Style Guide** - Visual documentation of all components and tokens

## Quick Start

```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview
```

Open [http://localhost:4321](http://localhost:4321) to see the demo homepage.

Visit [http://localhost:4321/style-guide](http://localhost:4321/style-guide) to explore all components.

## Project Structure

```
src/
├── components/
│   ├── atoms/              # Basic building blocks
│   │   ├── Button.astro    # Buttons with variants & sizes
│   │   ├── Input.astro     # Form inputs & textareas
│   │   ├── Badge.astro     # Status labels & tags
│   │   ├── Text.astro      # Typography component
│   │   └── index.ts        # Barrel export
│   │
│   ├── molecules/          # Combinations of atoms
│   │   ├── Card.astro      # Content container with slots
│   │   ├── FormField.astro # Label + input + helper text
│   │   ├── NavLink.astro   # Navigation link with active state
│   │   └── index.ts
│   │
│   ├── organisms/          # Complex UI sections
│   │   ├── Header.astro    # Site header with nav
│   │   ├── Footer.astro    # Site footer
│   │   ├── Section.astro   # Page section wrapper
│   │   └── index.ts
│   │
│   └── templates/          # Page-level layouts
│       ├── BaseLayout.astro # HTML document structure
│       └── index.ts
│
├── styles/
│   ├── design-system/
│   │   ├── tokens.css      # Design tokens (colors, spacing, etc.)
│   │   ├── typography.css  # Text styles & prose
│   │   ├── spacing.css     # Margin, padding, gap utilities
│   │   └── layout.css      # Flexbox, grid, container utilities
│   │
│   ├── base/
│   │   ├── reset.css       # Modern CSS reset
│   │   └── global.css      # Base element styles
│   │
│   └── main.css            # Entry point (imports all styles)
│
└── pages/
    ├── index.astro         # Demo homepage
    └── style-guide.astro   # Component documentation
```

## Design System

### Design Tokens

All visual properties are defined as CSS custom properties in `src/styles/design-system/tokens.css`. This single file controls the entire look and feel of your site.

#### Colors

```css
/* Primary palette */
--color-primary-50 through --color-primary-950

/* Neutral palette */
--color-neutral-0 through --color-neutral-950

/* Semantic colors */
--color-success-{50,500,700}
--color-warning-{50,500,700}
--color-error-{50,500,700}

/* Semantic assignments */
--color-text-primary, --color-text-secondary, --color-text-tertiary
--color-bg-primary, --color-bg-secondary, --color-bg-tertiary
--color-border-default, --color-border-strong, --color-border-focus
```

#### Spacing

Based on a 4px grid system:

```css
--space-1: 0.25rem;   /* 4px */
--space-2: 0.5rem;    /* 8px */
--space-3: 0.75rem;   /* 12px */
--space-4: 1rem;      /* 16px */
--space-6: 1.5rem;    /* 24px */
--space-8: 2rem;      /* 32px */
/* ... up to --space-32 */
```

#### Typography

```css
/* Font families */
--font-family-sans
--font-family-serif
--font-family-mono

/* Font sizes (modular scale) */
--font-size-xs through --font-size-6xl

/* Font weights */
--font-weight-light, normal, medium, semibold, bold

/* Line heights */
--line-height-none, tight, snug, normal, relaxed, loose
```

#### Other Tokens

```css
/* Border radius */
--radius-sm, md, lg, xl, 2xl, 3xl, full

/* Shadows */
--shadow-xs, sm, md, lg, xl, 2xl

/* Transitions */
--transition-fast, normal, slow

/* Z-index scale */
--z-dropdown, sticky, fixed, modal, popover, tooltip
```

### Customization

#### Global Customization

Override tokens in `tokens.css` or create a new file and import it after `tokens.css` in `main.css`:

```css
/* src/styles/overrides/brand.css */
:root {
  /* Change the entire color scheme */
  --color-primary-500: #6366f1;
  --color-primary-600: #4f46e5;
  --color-primary-700: #4338ca;

  /* Change typography */
  --font-family-sans: 'Inter', system-ui, sans-serif;

  /* Adjust spacing scale */
  --space-4: 1.125rem;
}
```

#### Component-Level Customization

Each component exposes its own CSS variables for fine-grained control:

```css
/* Customize buttons globally */
:root {
  --btn-border-radius: var(--radius-full);
  --btn-font-weight: var(--font-weight-semibold);
  --btn-primary-bg: var(--color-primary-500);
  --btn-primary-bg-hover: var(--color-primary-600);
}

/* Customize cards */
:root {
  --card-border-radius: var(--radius-xl);
  --card-padding: var(--space-8);
  --card-elevated-shadow: var(--shadow-lg);
}
```

#### Per-Instance Customization

Override variables inline for specific instances:

```astro
<Button
  style="--btn-primary-bg: #10b981; --btn-border-radius: 0;"
>
  Custom Button
</Button>
```

## Components

### Atoms

#### Button

```astro
---
import Button from '@atoms/Button.astro';
---

<!-- Variants -->
<Button variant="primary">Primary</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="ghost">Ghost</Button>

<!-- Sizes -->
<Button size="sm">Small</Button>
<Button size="md">Medium</Button>
<Button size="lg">Large</Button>

<!-- As link -->
<Button as="a" href="/about">Link Button</Button>

<!-- States -->
<Button disabled>Disabled</Button>
<Button fullWidth>Full Width</Button>
```

**CSS Variables:**
- `--btn-font-family`, `--btn-font-weight`, `--btn-border-radius`
- `--btn-padding-{sm,md,lg}`, `--btn-font-size-{sm,md,lg}`
- `--btn-{primary,secondary,ghost}-bg`, `--btn-{variant}-color`, `--btn-{variant}-border`
- `--btn-{variant}-bg-hover`, `--btn-{variant}-border-hover`

#### Input

```astro
---
import Input from '@atoms/Input.astro';
---

<Input name="email" type="email" placeholder="Enter email" />
<Input name="message" as="textarea" rows={4} />
<Input name="search" size="lg" />
<Input name="error-field" error />
```

**CSS Variables:**
- `--input-font-family`, `--input-border-radius`, `--input-border-width`
- `--input-padding-{sm,md,lg}`, `--input-font-size-{sm,md,lg}`
- `--input-bg`, `--input-color`, `--input-border-color`
- `--input-focus-border-color`, `--input-focus-ring-color`
- `--input-error-border-color`, `--input-error-ring-color`

#### Badge

```astro
---
import Badge from '@atoms/Badge.astro';
---

<Badge>Default</Badge>
<Badge variant="primary">Primary</Badge>
<Badge variant="success">Success</Badge>
<Badge variant="warning">Warning</Badge>
<Badge variant="error">Error</Badge>

<Badge size="sm">Small</Badge>
<Badge size="lg">Large</Badge>
```

#### Text

```astro
---
import Text from '@atoms/Text.astro';
---

<Text as="h1" variant="heading-1">Page Title</Text>
<Text variant="body-large">Large body text</Text>
<Text variant="caption" color="secondary">Caption text</Text>
```

### Molecules

#### Card

```astro
---
import Card from '@molecules/Card.astro';
---

<!-- Basic -->
<Card>
  <h3>Card Title</h3>
  <p>Card content</p>
</Card>

<!-- With slots -->
<Card>
  <img slot="media" src="/image.jpg" alt="" />
  <div slot="header">Header</div>
  Content here
  <div slot="footer">Footer</div>
</Card>

<!-- Variants -->
<Card variant="elevated">Shadow elevation</Card>
<Card variant="outlined">Border outline</Card>
<Card variant="filled">Background fill</Card>

<!-- Interactive -->
<Card interactive>Clickable card</Card>
<Card href="/page">Link card</Card>
```

#### FormField

```astro
---
import FormField from '@molecules/FormField.astro';
---

<FormField
  label="Email Address"
  name="email"
  type="email"
  placeholder="you@example.com"
  helperText="We'll never share your email."
  required
/>

<FormField
  label="Password"
  name="password"
  type="password"
  errorText="Password must be at least 8 characters."
/>

<FormField
  label="Message"
  name="message"
  as="textarea"
  rows={4}
/>
```

#### NavLink

```astro
---
import NavLink from '@molecules/NavLink.astro';
---

<nav>
  <NavLink href="/">Home</NavLink>
  <NavLink href="/about">About</NavLink>
  <NavLink href="/blog" exact={false}>Blog</NavLink>
</nav>
```

### Organisms

#### Header

```astro
---
import Header from '@organisms/Header.astro';
import NavLink from '@molecules/NavLink.astro';
import Button from '@atoms/Button.astro';
---

<Header siteName="My Site" sticky>
  <nav slot="nav">
    <NavLink href="/">Home</NavLink>
    <NavLink href="/about">About</NavLink>
  </nav>
  <div slot="actions">
    <Button size="sm">Sign In</Button>
  </div>
</Header>
```

#### Footer

```astro
---
import Footer from '@organisms/Footer.astro';
---

<Footer siteName="My Site">
  <div slot="default">
    <!-- Footer content columns -->
  </div>
  <nav slot="nav">
    <a href="/privacy">Privacy</a>
    <a href="/terms">Terms</a>
  </nav>
  <div slot="social">
    <a href="https://twitter.com">Twitter</a>
  </div>
</Footer>
```

#### Section

```astro
---
import Section from '@organisms/Section.astro';
---

<Section
  title="Features"
  subtitle="What we offer"
  background="muted"
  size="lg"
  centerHeading
>
  <!-- Section content -->
</Section>
```

### Templates

#### BaseLayout

```astro
---
import BaseLayout from '@templates/BaseLayout.astro';
---

<BaseLayout
  title="Page Title"
  description="Page description for SEO"
>
  <main>
    <!-- Page content -->
  </main>
</BaseLayout>
```

## Path Aliases

The project includes TypeScript path aliases for cleaner imports:

```typescript
// Available aliases
@/*           → src/*
@components/* → src/components/*
@atoms/*      → src/components/atoms/*
@molecules/*  → src/components/molecules/*
@organisms/*  → src/components/organisms/*
@templates/*  → src/components/templates/*
@styles/*     → src/styles/*
```

Usage:

```astro
---
import Button from '@atoms/Button.astro';
import Card from '@molecules/Card.astro';
import Header from '@organisms/Header.astro';
import BaseLayout from '@templates/BaseLayout.astro';
---
```

## Adding New Components

### 1. Create the Component

Create a new `.astro` file in the appropriate atomic level folder:

```astro
---
// src/components/atoms/Avatar.astro

interface Props {
  src: string;
  alt: string;
  size?: 'sm' | 'md' | 'lg';
  class?: string;
}

const { src, alt, size = 'md', class: className = '' } = Astro.props;
---

<img
  class={`avatar avatar--${size} ${className}`}
  src={src}
  alt={alt}
/>

<style>
  .avatar {
    border-radius: var(--avatar-border-radius, var(--radius-full));
    object-fit: cover;
  }

  .avatar--sm {
    width: var(--avatar-size-sm, 32px);
    height: var(--avatar-size-sm, 32px);
  }

  .avatar--md {
    width: var(--avatar-size-md, 48px);
    height: var(--avatar-size-md, 48px);
  }

  .avatar--lg {
    width: var(--avatar-size-lg, 64px);
    height: var(--avatar-size-lg, 64px);
  }
</style>
```

### 2. Export from Index

Add to the barrel export file:

```typescript
// src/components/atoms/index.ts
export { default as Avatar } from './Avatar.astro';
```

### 3. Document in Style Guide

Add a section to `src/pages/style-guide.astro` showcasing the component.

## Best Practices

### Component Design

1. **Use CSS variables with fallbacks** - Always provide a default value:
   ```css
   background: var(--btn-bg, var(--color-primary-600));
   ```

2. **Namespace component variables** - Prefix with component name:
   ```css
   --card-padding, --btn-border-radius, --input-focus-color
   ```

3. **Accept a `class` prop** - Allow consumers to add custom classes:
   ```astro
   const { class: className = '' } = Astro.props;
   <div class={`component ${className}`}>
   ```

4. **Use slots for flexibility** - Let consumers control content structure:
   ```astro
   <slot name="header" />
   <slot />
   <slot name="footer" />
   ```

### CSS Organization

1. **Tokens first** - Define all values in `tokens.css`
2. **Semantic variables** - Map primitives to semantic uses
3. **Component variables** - Reference semantic variables in components
4. **Utility classes** - Use sparingly for common patterns

### Accessibility

1. **Focus states** - All interactive elements have visible focus styles
2. **Color contrast** - Semantic colors meet WCAG AA standards
3. **Reduced motion** - Animations respect `prefers-reduced-motion`
4. **Semantic HTML** - Components use appropriate elements

## Dark Mode

Dark mode support is prepared but commented out in `tokens.css`. To enable:

1. Uncomment the `@media (prefers-color-scheme: dark)` block in `tokens.css`
2. Or implement a manual toggle by adding a `.dark` class to `<html>` and updating the selector

```css
/* Automatic dark mode */
@media (prefers-color-scheme: dark) {
  :root {
    --color-text-primary: var(--color-neutral-100);
    --color-bg-primary: var(--color-neutral-900);
    /* ... */
  }
}

/* Manual toggle */
html.dark {
  --color-text-primary: var(--color-neutral-100);
  --color-bg-primary: var(--color-neutral-900);
  /* ... */
}
```

## Browser Support

This starter uses modern CSS features supported in all evergreen browsers:

- CSS Custom Properties (variables)
- CSS Grid and Flexbox
- `aspect-ratio`
- `gap` in flexbox
- `:focus-visible`

For older browser support, consider using PostCSS with appropriate plugins.

## Commands

| Command             | Action                                       |
| :------------------ | :------------------------------------------- |
| `npm install`       | Install dependencies                         |
| `npm run dev`       | Start dev server at `localhost:4321`         |
| `npm run build`     | Build production site to `./dist/`           |
| `npm run preview`   | Preview production build locally             |
| `npm run astro ...` | Run Astro CLI commands                       |

## License

MIT License - feel free to use this starter for any project.

---

Built with [Astro](https://astro.build)
