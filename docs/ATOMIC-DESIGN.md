# Atomic Design in This Project

This document explains how the atomic design methodology is applied in this Astro starter template.

## What is Atomic Design?

Atomic Design is a methodology for creating design systems, introduced by Brad Frost. It breaks down interfaces into fundamental building blocks and organizes them into five distinct levels:

1. **Atoms** - Basic building blocks
2. **Molecules** - Simple groups of atoms
3. **Organisms** - Complex components
4. **Templates** - Page-level layouts
5. **Pages** - Specific instances of templates

This project uses four levels (atoms through templates), with pages handled by Astro's built-in routing.

---

## Levels in This Project

### Atoms

**Location:** `src/components/atoms/`

Atoms are the smallest, most fundamental components. They cannot be broken down further without losing their meaning as UI elements.

**Characteristics:**
- Single-purpose
- No child components (other than slot content)
- Highly reusable
- Style-agnostic (customizable via CSS variables)

**Current Atoms:**
| Component | Purpose |
|-----------|---------|
| `Button` | Clickable action element |
| `Input` | Text input and textarea |
| `Badge` | Status label or tag |
| `Text` | Typography wrapper |

**Examples of potential atoms:**
- `Icon` - SVG icon wrapper
- `Avatar` - User profile image
- `Checkbox` - Form checkbox
- `Radio` - Form radio button
- `Toggle` - On/off switch
- `Spinner` - Loading indicator
- `Divider` - Horizontal rule
- `Image` - Responsive image

### Molecules

**Location:** `src/components/molecules/`

Molecules are simple combinations of atoms that work together as a unit. They have a single responsibility but are composed of multiple parts.

**Characteristics:**
- Combines 2-3 atoms
- Single responsibility
- Self-contained
- Commonly reused patterns

**Current Molecules:**
| Component | Composition | Purpose |
|-----------|-------------|---------|
| `Card` | Container + slots | Content grouping |
| `FormField` | Label + Input + helper | Complete form field |
| `NavLink` | Link with active detection | Navigation item |

**Examples of potential molecules:**
- `SearchInput` - Input + Button + Icon
- `MediaObject` - Image + Text content
- `Stat` - Label + Value + Change indicator
- `Breadcrumb` - Series of links
- `Pagination` - Page navigation
- `Toast` - Notification message
- `Modal` - Dialog container
- `Dropdown` - Trigger + Menu

### Organisms

**Location:** `src/components/organisms/`

Organisms are complex UI components composed of atoms, molecules, and/or other organisms. They form distinct sections of an interface.

**Characteristics:**
- Multiple responsibilities
- Self-contained sections
- Often context-aware
- Page-section level

**Current Organisms:**
| Component | Composition | Purpose |
|-----------|-------------|---------|
| `Header` | Logo + NavLinks + Buttons | Site header |
| `Footer` | Copyright + NavLinks + Social | Site footer |
| `Section` | Title + Content container | Page section |

**Examples of potential organisms:**
- `Hero` - Headline + Subhead + CTAs + Image
- `FeatureGrid` - Section + Cards
- `Testimonials` - Section + Quotes
- `PricingTable` - Cards with pricing
- `ContactForm` - Form fields + Button
- `Newsletter` - Input + Button + Text
- `Sidebar` - Navigation + Widgets
- `ArticleCard` - Card with image, meta, excerpt

### Templates

**Location:** `src/components/templates/`

Templates define the overall page structure and layout. They arrange organisms and provide the HTML document structure.

**Characteristics:**
- Page-level structure
- HTML document boilerplate
- Global styles injection
- Common elements (header/footer)

**Current Templates:**
| Component | Purpose |
|-----------|---------|
| `BaseLayout` | Standard page with header/footer |

**Examples of potential templates:**
- `BlogLayout` - Article page with sidebar
- `LandingLayout` - Marketing page without nav
- `DashboardLayout` - App layout with sidebar
- `AuthLayout` - Minimal login/signup page
- `DocsLayout` - Documentation with TOC

---

## Component Relationships

```
Templates
    └── contain → Organisms
                      └── contain → Molecules
                                        └── contain → Atoms
```

### Example: Contact Page

```
BaseLayout (Template)
├── Header (Organism)
│   ├── Logo (Atom - could be Image)
│   ├── NavLink (Molecule) × 4
│   └── Button (Atom)
├── Section (Organism)
│   ├── Text (Atom) - Title
│   └── Text (Atom) - Subtitle
├── Card (Molecule)
│   ├── FormField (Molecule)
│   │   ├── Label (implicit)
│   │   └── Input (Atom)
│   ├── FormField (Molecule)
│   │   └── Input (Atom) as textarea
│   └── Button (Atom)
└── Footer (Organism)
    ├── Text (Atom) - Copyright
    └── NavLink (Molecule) × 3
```

---

## Decision Guide

### When to Create an Atom

Create an atom when:
- It's a native HTML element wrapper (button, input, img)
- It cannot be meaningfully split further
- It's used in many different contexts
- It has no awareness of its siblings

### When to Create a Molecule

Create a molecule when:
- You're combining 2-3 atoms that always go together
- The combination is reused in multiple places
- It has a single, clear purpose
- It's still relatively simple

### When to Create an Organism

Create an organism when:
- It's a complete section of a page
- It combines multiple molecules/atoms
- It has its own internal logic or state
- It represents a distinct UI region

### When to Create a Template

Create a template when:
- It defines overall page structure
- It includes HTML document elements (head, body)
- It provides the layout for a type of page
- It determines which organisms appear where

---

## Practical Tips

### 1. Start with Atoms

When building a new feature, identify the atomic pieces first:
- What buttons do I need?
- What inputs?
- What text styles?

### 2. Find Repeated Patterns

Look for combinations that repeat:
- "I always put a label above an input" → `FormField` molecule
- "Cards always have this structure" → `Card` molecule

### 3. Don't Over-Atomize

Not everything needs to be a component:
- A single `<p>` tag doesn't need a wrapper
- Native HTML is fine for simple cases
- Only abstract when there's reuse or complexity

### 4. Keep Atoms Pure

Atoms shouldn't know about:
- Their parent component
- Application state
- Business logic
- Layout (their container handles positioning)

### 5. Use Slots for Flexibility

Prefer slots over complex prop APIs:

```astro
<!-- Good: Flexible via slots -->
<Card>
  <img slot="media" src="..." />
  <h3>Title</h3>
  <p>Content</p>
</Card>

<!-- Avoid: Rigid prop-based API -->
<Card
  imageSrc="..."
  title="Title"
  content="Content"
/>
```

---

## Resources

- [Atomic Design by Brad Frost](https://atomicdesign.bradfrost.com/)
- [Atomic Design Methodology](https://atomicdesign.bradfrost.com/chapter-2/)
- [Pattern Lab](https://patternlab.io/) - Tool for atomic design
