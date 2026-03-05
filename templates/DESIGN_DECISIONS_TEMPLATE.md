# Design Decisions Log

**Project**: [Your Project Name]
**Date Started**: [Date]
**Last Updated**: [Date]

This document logs all design-to-code decisions, rationale, trade-offs, and validation for this project. Use this to maintain design fidelity across the codebase and preserve institutional knowledge.

---

## Table of Contents

- [Design System Decisions](#design-system-decisions)
- [Component Decisions](#component-decisions)
- [Animation Standards](#animation-standards)
- [Validation Summary](#validation-summary)

---

## Design System Decisions

### Color System

**Decision**: Used CSS custom properties (variables) for all colors with light/dark mode support.

**Rationale**:
- Single source of truth for all brand colors
- Zero-runtime switching for dark mode (CSS-only)
- Easy to update globally without rebuilding
- Enables accessible color contrast checking

**Code**:
```css
:root {
  /* Light mode defaults */
  --color-primary: #0f0d0a;
  --color-primary-text: #fefefe;
  --color-bg: #fefefe;
  --color-text: #0f0d0a;
}

[data-theme="dark"] {
  --color-primary: #fefefe;
  --color-primary-text: #0f0d0a;
  --color-bg: #0f0d0a;
  --color-text: #fefefe;
}
```

**Trade-offs**:
- CSS variables not supported in IE11 (acceptable if not targeting legacy browsers)
- Can't be used in build-time optimization (only runtime)

**Validation**:
✓ Color contrast checked with aXe DevTools
✓ Tested light → dark → light transitions
✓ No flashing on page load
✓ All components using variables, zero hardcoded colors

---

### Typography Scale

**Decision**: Defined typography as CSS variables with fixed pixel values (no fluid scaling).

**Rationale**:
- Predictable, consistent sizing across all screens
- Easier to maintain and test
- Buttons and inputs need fixed heights for accessibility
- Simplicity > complexity

**Code**:
```css
:root {
  --font-primary: 'EB Garamond', serif;
  --font-mono: 'DM Mono', monospace;

  --font-size-xs: 12px;
  --font-size-sm: 14px;
  --font-size-base: 16px;
  --font-size-lg: 18px;
  --font-size-xl: 24px;
  --font-size-2xl: 32px;
}
```

**Alternatives Considered**:
1. **Fluid typography** using `clamp(min, preferred, max)`
   - Pro: Responsive without media queries
   - Con: Can feel unpredictable at edge sizes

2. **Em-based scaling** (relative to parent)
   - Pro: Component-level control
   - Con: Harder to maintain, inheritance issues

**Trade-offs**:
- Media queries needed for responsive typography adjustments
- Less flexibility for unique per-page sizing

**Validation**:
✓ All font sizes match Pencil specs exactly
✓ Line heights tested for readability (1.4-1.6 for body)
✓ Heading hierarchy clear and distinct
✓ Mobile, tablet, desktop sizes verified

---

### Spacing & Grid

**Decision**: All spacing uses 8px grid with CSS variables.

**Rationale**:
- 8px is industry standard, familiar to designers and developers
- Simplifies mental math (8, 16, 24, 32, 40, 48...)
- Enforces visual consistency
- Easy to audit (all values divisible by 8)

**Code**:
```css
:root {
  --spacing-0: 0;
  --spacing-1: 8px;
  --spacing-2: 16px;
  --spacing-3: 24px;
  --spacing-4: 32px;
  --spacing-5: 40px;
  --spacing-6: 48px;
}
```

**Rule**: All padding, margin, gap, and gaps must use these variables. Zero hardcoded pixel values.

**Validation**:
✓ Audited every component for 8px alignment
✓ No odd values like 13px, 27px, 35px found
✓ All gaps between elements respect grid
✓ Responsive adjustments tested on mobile

---

## Component Decisions

### Button Component

**Decision**: Used CSS modules + BEM naming for variants and sizes.

**Rationale**:
- Variants as class modifiers (primary, secondary, ghost) vs separate components
  - Easier to compose (one component, 9 combinations)
  - Smaller bundle (1 component vs 3)
- Props-based API makes usage explicit and discoverable

**Code**:
```tsx
<Button variant="primary" size="md">Click me</Button>
```

**CSS**:
```css
.button { /* base */ }
.button.primary { /* variant */ }
.button.md { /* size */ }
```

**Alternatives Considered**:
1. **Separate components** (PrimaryButton, SecondaryButton)
   - Con: Duplication, harder to maintain

2. **Compound components** (Button.Primary)
   - Con: More complex, not needed here

3. **CSS-in-JS** (styled-components)
   - Con: Runtime overhead, static variants don't need it

**Trade-offs**:
- Can't mix variants (intentional — a button shouldn't be both primary and secondary)
- If adding 15+ variants, might reconsider approach

**Validation**:
✓ All spec heights match: sm=32, md=44, lg=56
✓ All spec padding exact: sm="8px 12px", md="12px 16px", lg="16px 24px"
✓ 44px touch target passes WCAG AAA
✓ Color contrast >= 4.5:1 (AA compliance)
✓ Disabled state clear (opacity + cursor)

---

### Card Component

**Decision**: Cards use elevation (shadow) only when needed for hierarchy. Avoid "card boxes" everywhere.

**Rationale**:
- Cards everywhere = visual noise
- Use spacing and borders for most grouping
- Reserve elevation for truly stacked content
- Simpler CSS, smaller bundle

**Rule**: Cards (with shadows) only for:
- Modals and overlays
- Floating panels above content
- Deeply nested sections

**Validation**:
✓ Dashboard uses borders + spacing, zero shadow cards
✓ Only modals have elevated cards
✓ Visual hierarchy clear without overuse

---

## Animation Standards

### List & Collection Animations

**Standard Pattern**:
```typescript
{items.map((item, idx) => (
  <motion.div
    key={idx}
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    transition={{
      duration: 0.3,
      delay: idx * 0.05,
      ease: [0.25, 0.46, 0.45, 0.94]
    }}
  >
    {/* Content */}
  </motion.div>
))}
```

**Rules** (MUST follow exactly):
- **Duration**: 0.3s (no variations)
- **Easing**: `[0.25, 0.46, 0.45, 0.94]` (cubic-bezier standard)
- **Stagger**: `idx * 0.05` (50ms between items)
- **Entry**: opacity only (NO transforms)
- **Container**: Wrap with `<AnimatePresence>` when list changes

**Applied to**: Chat messages, cards, discovery items, history lists

**Decision Rationale**:
- Consistent timing across entire app (not per-page)
- 0.3s fast enough for frequent actions
- 50ms stagger visible without feeling slow
- Opacity-only prevents layout shift jank

**Validation**:
✓ All lists use same pattern
✓ No spring physics on list items
✓ No mixed durations
✓ Timing feels cohesive

---

### Page Transitions

**Standard Pattern**:
```typescript
<motion.div
  key={pathname}
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{
    duration: 0.5,
    ease: [0.25, 0.46, 0.45, 0.94]
  }}
>
  {children}
</motion.div>
```

**Rules** (MUST follow):
- **Duration**: ALWAYS 0.5s
- **Easing**: `[0.25, 0.46, 0.45, 0.94]`
- **No exit animations** (prevents double fade)
- **Key change** triggers animation on route change

**Decision Rationale**:
- 0.5s longer than list animations for page-level importance
- No exit prevents stutter when transitioning routes
- Key={pathname} ensures fresh animation on each page

**Validation**:
✓ No page transition flicker
✓ Consistent timing across all pages
✓ Exit animations removed (smooth transitions)

---

### Bottom Sheets

**Standard Pattern**:
```typescript
<AnimatePresence>
  <motion.div
    initial={{ y: '100%' }}
    animate={{ y: 0, transition: { type: 'spring', damping: 30, stiffness: 300 } }}
    exit={{ y: '100%', transition: { duration: 0.2 } }}
  >
    {/* Staggered children */}
  </motion.div>
</AnimatePresence>
```

**Rules**:
- **Entry**: Spring physics (not linear fade)
- **Exit**: 0.2s slide down
- **Children**: Stagger 0.1s between items

**Decision Rationale**:
- Spring entry feels responsive and playful
- Exit is quick (0.2s) to not block navigation
- Child stagger reveals content progressively

**Validation**:
✓ All bottom sheets use this pattern
✓ Spring timing consistent
✓ No custom sheet implementations

---

## Validation Summary

### Structural ✓
- [x] Component names match Pencil specs
- [x] Props align with design variations
- [x] DOM hierarchy is semantic
- [x] Accessibility: WCAG AA minimum on all interactive elements

### Visual Fidelity ✓
- [x] Typography: Font families, sizes, weights match spec
- [x] Colors: All CSS variables, zero hardcoded hex
- [x] Spacing: 100% of values on 8px grid
- [x] Alignment: Flexbox/Grid matches visual design
- [x] Border radius: Consistent with system

### Pixel-Perfect Specs ✓
- [x] Component dimensions exact
- [x] Padding/margin values precise
- [x] Gaps between elements correct
- [x] Responsive breakpoints implemented
- [x] Dark/light mode working

### Animation Standards ✓
- [x] List items: fade only, 0.3s, 50ms stagger
- [x] Page transitions: fade, 0.5s, no exit
- [x] Bottom sheets: spring entry, slide exit
- [x] Easing: consistent cubic-bezier across all

### Code Quality ✓
- [x] No inline styles
- [x] No hardcoded colors or spacing
- [x] No console warnings
- [x] Builds without errors
- [x] Clean, readable code

---

## Next Component to Document

**Component**: [Component name]
**Status**: 🟡 In progress / 🟢 Completed / 🔴 Blocked

Use this template for each new component added to the system.
