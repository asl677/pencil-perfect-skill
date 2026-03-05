![Prfct Logo](./logo.png)

# Pencil-Perfect: Design-to-Code at Production Scale

Convert **Pencil designs** → **Pixel-perfect React/Next.js code** with automatic validation, component extraction, and design decision documentation.

Built for teams that demand both **design fidelity** and **code quality**. No manual specs. No guessing. Just pixel-perfect implementations.

---

## Why Pencil-Perfect?

### The Problem
Most design-to-code workflows break down at scale:
- Designers hand off specs; developers ignore them
- Animations are inconsistent across pages
- Design tokens aren't enforced in code
- "Pixel-perfect" claims don't hold up in production

### The Solution
**Pencil-Perfect** is a systematic workflow that:

✅ **Extracts specifications** from Pencil designs (components, tokens, spacing, typography)
✅ **Generates code** that matches specs exactly (React, TypeScript, Tailwind CSS)
✅ **Validates at 3 layers**: structure, visual fidelity, pixel-perfect measurements
✅ **Documents design decisions** so future changes don't break the system
✅ **Enforces animation standards** (no more inconsistent timings/easing)
✅ **Integrates with Claude Code** for collaborative refinement

---

## Quick Start

### 1. Export Your Design from Pencil
```json
{
  "project": {
    "name": "my-app",
    "designSystem": {
      "spacing": "8px grid",
      "colors": {
        "light": { "bg": "#fefefe", "text": "#0f0d0a" },
        "dark": { "bg": "#0f0d0a", "text": "#fefefe" }
      }
    },
    "components": [
      {
        "name": "Button",
        "variants": ["primary", "secondary"],
        "measurements": { "padding": "12px 16px", "height": 44 }
      }
    ]
  }
}
```

### 2. Generate Code
Paste specs into Claude Code with the **Pencil-Perfect skill**:

```
Using these Pencil specs:
[PASTE SPECS HERE]

Generate pixel-perfect React components using Pencil-Perfect standards:
- CSS variables for all design tokens
- Exact measurements from specs
- Animation patterns: 0.3s lists, 0.5s pages
- Semantic HTML + accessibility
- No hardcoded values
```

### 3. Validate & Deploy
Run the validation checklist (see SKILL.md):
- [ ] Structure: Component hierarchy matches design
- [ ] Visual: Typography, colors, spacing precise
- [ ] Specs: All measurements exactly match design
- [ ] Animations: Consistent timing, easing, stagger

---

## Core Concepts

### 3-Layer Validation

**Layer 1: Structural**
- Component names and props match design
- DOM hierarchy is semantic
- No prop drilling beyond 2 levels

**Layer 2: Visual Fidelity**
- Font families, sizes, weights correct
- Colors use CSS variables
- Spacing aligns to 8px grid
- Alignment matches design intent

**Layer 3: Pixel-Perfect Specs**
- Exact dimensions (width, height, padding)
- Precise measurements from design
- Responsive breakpoints implemented
- Dark/light mode working

### Animation Standards

Every animation follows the same rules for consistency:

| Context | Duration | Easing | Stagger | Pattern |
|---------|----------|--------|---------|---------|
| **Lists** | 0.3s | `[0.25, 0.46, 0.45, 0.94]` | `idx * 0.05` | Fade only (opacity) |
| **Page transitions** | 0.5s | `[0.25, 0.46, 0.45, 0.94]` | N/A | Fade, no exit |
| **Bottom sheets** | Spring | `damping: 30, stiffness: 300` | N/A | Slide up/down |
| **Micro-interactions** | 0.2-0.4s | `[0.25, 0.46, 0.45, 0.94]` | N/A | Context-dependent |

**Forbidden:**
- ❌ Different easing per component
- ❌ Spring physics on lists
- ❌ Transform animations on list items
- ❌ Hardcoded pixel values anywhere
- ❌ Custom bottom sheets (use standard component)

### Design Decisions Documentation

Every component gets documented with:
- **Decision**: What choice was made?
- **Rationale**: Why this over alternatives?
- **Trade-offs**: What are the costs?
- **Validation**: How was it verified?

Example:
```markdown
## Button Component

### Decision
Used CSS modules + BEM naming for variants.

### Rationale
- Variants as class modifiers vs separate components
  - Easier to compose (one component, infinite combinations)
  - Smaller bundle size

### Trade-offs
- Can't mix variant + size in same element (by design)

### Validation
✓ All spec values match exactly
✓ Colors match on light + dark themes
✓ 44px height passes WCAG touch target
```

---

## File Structure

```
my-project/
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.module.css
│   │   └── Button.stories.tsx
│   └── Card/
│       ├── Card.tsx
│       └── Card.module.css
├── design-system/
│   ├── tokens.css       # --color-, --spacing-, --font- vars
│   └── global.css
├── docs/
│   └── DESIGN_DECISIONS.md
├── .claude/
│   └── CLAUDE.md        # Project-specific rules
└── package.json
```

---

## What Gets Validated

### ✅ Structure
- Component hierarchy matches Pencil
- Props API complete and documented
- Semantic HTML throughout
- No accessibility issues (WCAG AA minimum)

### ✅ Visual Fidelity
- Typography exact (font, size, weight, line-height)
- Colors via CSS variables only
- Spacing on 8px grid
- Alignment via Flexbox/Grid

### ✅ Pixel-Perfect Specs
- Heights, widths match design exactly
- Padding/margin values precise
- Gaps between elements correct
- Responsive breakpoints working
- Dark/light mode complete

### ✅ Animations
- List items fade in with 50ms stagger
- Page transitions smooth (no double fade)
- Bottom sheets slide smoothly
- Timings consistent across the app
- Easing matches cubic-bezier standard

### ✅ Code Quality
- No hardcoded colors or spacing
- All values CSS variables
- No console warnings
- Builds without errors
- Clean, readable code

---

## Validation Checklist Template

Copy this to your project's `DESIGN_DECISIONS.md`:

```markdown
# Design Validation

## Structure
- [ ] Component names match Pencil specs
- [ ] Props align with design variations
- [ ] DOM hierarchy is semantic
- [ ] No prop drilling beyond 2 levels

## Visual Fidelity
- [ ] Typography exact (font, size, weight, line-height)
- [ ] Colors: All CSS variables, no hardcoded hex
- [ ] Spacing: All values on 8px grid
- [ ] Alignment: Flexbox/Grid matches visual
- [ ] Border radius: Consistent with system

## Pixel-Perfect Specs
- [ ] Component dimensions exact (height, width)
- [ ] Padding/margin values precise
- [ ] Gaps between child elements correct
- [ ] Responsive breakpoints implemented
- [ ] Dark/light mode variables working

## Animations (if applicable)
- [ ] List items use fade only (opacity: 0 → 1)
- [ ] Stagger delay is `idx * 0.05` (50ms)
- [ ] Duration: 0.3s for lists, 0.5s for pages
- [ ] Easing: `[0.25, 0.46, 0.45, 0.94]`
- [ ] Page transitions have NO exit animation
- [ ] Bottom sheets use spring + slide

## Code Quality
- [ ] No inline styles (use CSS classes)
- [ ] No magic numbers (use variables)
- [ ] Alt text on images, ARIA labels
- [ ] No console errors/warnings
- [ ] Builds without warnings

## Documentation
- [ ] Component API documented
- [ ] Props have JSDoc comments
- [ ] Design decisions logged
- [ ] Rationale documented
```

---

## Common Mistakes (Avoid These)

| ❌ Mistake | ✅ Fix |
|---|---|
| Different easing per component | Always use `[0.25, 0.46, 0.45, 0.94]` |
| Hardcoded `#fff` or `16px` | Use CSS variables everywhere |
| Spring physics on list items | Use fade only (opacity) |
| Custom bottom sheets | Use standard BottomSheet component |
| No animation specs in design | Document them in CLAUDE.md or DESIGN_DECISIONS.md |
| Animation durations vary | Use 0.3s lists, 0.5s pages consistently |
| Stagger delays arbitrary | Use `idx * 0.05` (50ms between items) |
| No validation checklist | Use the template above |

---

## Recommended Stack

| Layer | Technology | Why |
|-------|-----------|------|
| **Framework** | Next.js 14+ | Server Components, optimal DX |
| **Styling** | Tailwind CSS v4 | Utility-first, design tokens native |
| **Animation** | Framer Motion | Precise control, spring physics, layout animations |
| **Components** | React 18+ | Hooks, Suspense, error boundaries |
| **Type Safety** | TypeScript | Catch errors before runtime |
| **Design Tokens** | CSS Custom Properties | Live updates, no rebuild |

---

## Example: Button Component

### Pencil Spec
```json
{
  "name": "Button",
  "variants": {
    "primary": { "bg": "#0f0d0a", "text": "#fefefe" },
    "secondary": { "bg": "transparent", "border": "1px solid #0f0d0a", "text": "#0f0d0a" }
  },
  "sizes": {
    "sm": { "height": 32, "padding": "8px 12px", "fontSize": 12 },
    "md": { "height": 44, "padding": "12px 16px", "fontSize": 16 },
    "lg": { "height": 56, "padding": "16px 24px", "fontSize": 18 }
  }
}
```

### Generated Code
```tsx
// components/Button.tsx
import styles from './Button.module.css'

export function Button({
  variant = 'primary',
  size = 'md',
  disabled = false,
  children,
  ...props
}: {
  variant?: 'primary' | 'secondary'
  size?: 'sm' | 'md' | 'lg'
  disabled?: boolean
  children: React.ReactNode
} & React.ButtonHTMLAttributes<HTMLButtonElement>) {
  return (
    <button
      className={`${styles.button} ${styles[variant]} ${styles[size]}`}
      disabled={disabled}
      {...props}
    >
      {children}
    </button>
  )
}
```

```css
/* components/Button.module.css */
.button {
  font-family: var(--font-primary);
  border: none;
  border-radius: var(--radius-sm);
  cursor: pointer;
  transition: all 0.2s ease;
  font-weight: 500;
}

.primary {
  background-color: var(--color-primary);
  color: var(--color-primary-text);
}

.secondary {
  background-color: transparent;
  border: 1px solid var(--color-primary);
  color: var(--color-primary);
}

.sm {
  height: 32px;
  padding: var(--spacing-1) var(--spacing-2);
  font-size: var(--font-size-sm);
}

.md {
  height: 44px;
  padding: var(--spacing-3) var(--spacing-4);
  font-size: var(--font-size-md);
}

.lg {
  height: 56px;
  padding: var(--spacing-4) var(--spacing-6);
  font-size: var(--font-size-lg);
}
```

### Validation
✓ Heights: sm=32, md=44, lg=56 (exact match)
✓ Padding: sm="8px 12px", md="12px 16px", lg="16px 24px" (exact match)
✓ Font sizes: sm=12, md=16, lg=18 (exact match)
✓ Colors: Uses CSS variables, not hardcoded
✓ Touch target: 44px minimum for accessibility

---

## For Design Systems Teams

If you're building a design system or shared component library:

1. **Extract components from Pencil** using Pencil-Perfect
2. **Create Storybook stories** with all variants
3. **Document props and usage** with JSDoc comments
4. **Version control specs** in your DESIGN_DECISIONS.md
5. **Tag releases** when design specs change
6. **Notify consumers** of breaking changes

---

## Getting Help

- **See SKILL.md** for complete workflow documentation
- **Check examples/** for real project examples
- **Review templates/** for starting points

---

## License

Apache 2.0 (code) + CC-BY-4.0 (documentation)

---

## Made with ✓ for pixel-perfect design teams

Designed by [Prfct](https://prfct.com) | Built for [agentskills](https://agentskills.io)
