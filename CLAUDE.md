# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Commands

```bash
# Development
npm run dev        # Start dev server at localhost:4321
npm run build      # Build production site to ./dist/
npm run preview    # Preview production build locally

# Astro CLI
npm run astro ...  # Run any Astro CLI command
```

## Architecture Overview

This is an **Astro starter with a vanilla CSS design system** using an **atomic design component architecture**. The key architectural principle is building components that are fully customizable through CSS variables without framework dependencies.

### Atomic Design Structure

Components are organized by complexity level:

- **Atoms** (`src/components/atoms/`) - Basic building blocks with variant props (Button, Input, Badge, Avatar, Text)
- **Molecules** (`src/components/molecules/`) - Combinations of atoms, numbered for structural variants (Card1, Card2, FormField, NavLink)
- **Organisms** (`src/components/organisms/`) - Complex UI sections, always numbered (Header1, Footer1, Hero1, CTA1, Feature1, Section)
- **Templates** (`src/components/templates/`) - Page-level layouts (BaseLayout, MinimalLayout)

### Relume-Aligned Naming Convention

This project follows **Relume naming conventions** for Figma-to-code workflow:

**Numbers vs Props Rule:**
- **Numbers** = Different STRUCTURE/LAYOUT (different HTML arrangement)
- **Props** = Different CONFIGURATION (same structure, different styling)

**Naming by Level:**
- Atoms: Base name + variant props (`Button variant="primary"`)
- Molecules: `{Type}{Number}` (`Card1`, `Card2`, `Card3`)
- Organisms: `{Category}{Number}` (`Header1`, `Hero1`, `CTA1`)

**CSS Class Pattern:** `{component}{number}_{element}` (underscore separator)
```css
.hero1_heading { }
.cta2_grid { }
.card1_body { }
```

**When to create a new numbered variant:**
- Different HTML structure
- Different visual layout (centered vs split, single vs two-column)
- Different content arrangement

**When to use props instead:**
- Padding/spacing variations (`size`, `paddingTop`, `paddingBottom`)
- Background color changes (`background`)
- Alignment options (`align`, `centered`)
- Container width (`containerWidth`)

### Design System Architecture

The design system uses a **three-layer token architecture**:

1. **Primitive tokens** (`src/styles/design-system/tokens.css`) - Raw color scales, spacing scale, font sizes
2. **Semantic tokens** - Map primitives to usage contexts (`--color-text-primary`, `--color-bg-secondary`)
3. **Component tokens** - Component-specific variables that reference semantic tokens (`--btn-primary-bg`, `--card-padding`)

All components expose CSS variables for customization with fallbacks:
```css
background: var(--btn-bg, var(--color-primary-600));
```

CSS files in `src/styles/`:
- `design-system/tokens.css` - All design tokens (colors, spacing, typography, shadows, radii)
- `design-system/typography.css` - Text styles and prose formatting
- `design-system/spacing.css` - Margin, padding, gap utilities
- `design-system/layout.css` - Flexbox, grid, container utilities
- `base/reset.css` - Modern CSS reset
- `base/global.css` - Base element styles
- `main.css` - Entry point that imports all styles

### Content Collections

Uses **Astro Content Collections** for type-safe content management (`src/content/config.ts`):

- **Blog collection** (`src/content/blog/`) - Markdown posts with frontmatter schema (title, description, pubDate, heroImage, category reference, author, draft)
- **Categories collection** (`src/content/categories/`) - Category metadata (name, description, color)

**Important:** Blog post images should use `/images/blog/` paths (not `/blog/`) to avoid conflicts with the dynamic `[...slug].astro` route.

Dynamic routes use `getStaticPaths()` for pre-rendering:
- `src/pages/blog/[...slug].astro` - Individual blog posts
- `src/pages/category/[slug].astro` - Category archive pages

### Path Aliases

TypeScript aliases defined in `tsconfig.json`:

```typescript
@/*           → src/*
@components/* → src/components/*
@atoms/*      → src/components/atoms/*
@molecules/*  → src/components/molecules/*
@organisms/*  → src/components/organisms/*
@templates/*  → src/components/templates/*
@styles/*     → src/styles/*
```

Use in imports:
```astro
import Button from '@atoms/Button.astro';
import { Hero1, CTA1 } from '@organisms';
```

### Section Organism Pattern

All section organisms accept standard props for layout control:

```typescript
interface SectionProps {
  // Padding
  size?: 'sm' | 'md' | 'lg';
  paddingTop?: 'none' | 'sm' | 'md' | 'lg';
  paddingBottom?: 'none' | 'sm' | 'md' | 'lg';

  // Background
  background?: 'default' | 'muted' | 'primary' | 'dark';

  // Container
  contained?: boolean;
  containerWidth?: 'small' | 'medium' | 'large' | 'full';
}
```

These props override defaults set by the `Section` base component, allowing fine-grained layout control.

## Component Development Workflow

### Adding a New Component

1. **Determine the atomic level** - Atom (basic), Molecule (composite), or Organism (section)

2. **Check if a numbered variant is needed** - Only if structure differs significantly

3. **Create the .astro file** in the appropriate directory:
   ```astro
   ---
   interface Props {
     variant?: 'default' | 'outlined';
     class?: string;
     [key: string]: any;
   }

   const { variant = 'default', class: className = '', ...rest } = Astro.props;
   ---

   <div class={`component1 component1--${variant} ${className}`} {...rest}>
     <slot />
   </div>

   <style>
     .component1 {
       /* Use CSS variables with fallbacks */
       padding: var(--component1-padding, var(--space-4));
     }
   </style>
   ```

4. **Export from index.ts** in the same directory:
   ```typescript
   export { default as Component1 } from './Component1.astro';
   ```

5. **Update style guide** - Add showcase to `src/pages/style-guide.astro` if relevant

### Component Best Practices

- **Always accept a `class` prop** for custom classes
- **Namespace CSS variables** with component name (`--card1-padding`, not `--padding`)
- **Provide fallback values** for all CSS variables
- **Use slots** for flexibility (named slots: header, footer, media)
- **Follow BEM-like class naming** with underscore separator (`component1_element`)
- **Include section props** for organisms (size, paddingTop, paddingBottom, background)

### Customization Approach

Three levels of customization:

1. **Global tokens** - Override in `tokens.css` or create new file imported after it
2. **Component defaults** - Override component CSS variables globally in `:root`
3. **Per-instance** - Override inline via `style` attribute

## Static Assets

- `public/` directory is served at root path
- Images should go in `public/images/` subdirectories
- Blog hero images: `public/images/blog/` (referenced as `/images/blog/filename.jpg`)
- Favicon: `public/favicon.svg`

## Dark Mode

Dark mode tokens are prepared but commented out in `tokens.css`. To enable:

- Uncomment the `@media (prefers-color-scheme: dark)` block, or
- Implement manual toggle with `.dark` class on `<html>`

## Browser Support

Uses modern CSS features (CSS variables, Grid, Flexbox, `aspect-ratio`, `gap` in flexbox, `:focus-visible`). All supported in evergreen browsers.
