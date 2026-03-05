# Pencil-to-Code: Pixel-Perfect Design Workflow

Convert Pencil designs to production-ready code with automatic validation, component extraction, and comprehensive design documentation.

## Overview

This skill enables a flexible, mixed-mode workflow for design-to-code conversion:
- **Mode 1**: Pencil exports → Claude Code → validate visually
- **Mode 2**: Pencil AI agent → refine in Claude → validate specs
- **Mode 3**: Manual component mapping + code generation
- **Mode 4**: Hybrid (any combination above)

All paths include **three-layer validation** (structure, visual fidelity, pixel-perfect specs) and automatic **design decision logging** to your project's design doc.

---

## Workflow: Design → Code → Validate → Document

### Step 1: Extract Design Specifications from Pencil

**Input options:**
- `.pen` file (Pencil native format)
- Pencil export (JSON, SVG, or design tokens)
- Figma/design mockup imported into Pencil
- Manual component list + spacing grid

**Extract these specifications:**

```json
{
  "project": {
    "name": "project-name",
    "designSystem": {
      "spacing": "8px grid",
      "typography": {
        "families": ["DM Serif Display", "Inter"],
        "scales": [12, 14, 16, 18, 24, 32]
      },
      "colors": {
        "light": { "bg": "#fefefe", "text": "#0f0d0a" },
        "dark": { "bg": "#0f0d0a", "text": "#fefefe" }
      },
      "gridSize": 8,
      "borderRadius": "4px"
    },
    "components": [
      {
        "name": "Button",
        "variants": ["primary", "secondary", "ghost"],
        "props": { "size": ["sm", "md", "lg"], "state": ["default", "hover", "active"] },
        "measurements": {
          "padding": "12px 16px",
          "height": 44,
          "minWidth": 60
        }
      }
    ]
  }
}
```

**Questions to ask yourself:**
- Are there design tokens (colors, spacing, fonts) that should be variables?
- Which elements repeat across screens (components)?
- What responsive breakpoints exist?
- Are there animation/interaction specs?

### Step 2: Generate Code (Mixed Workflow Support)

Choose your generation path:

#### Path A: Direct Pencil Export → Code
1. Export design specs from Pencil (use AI agent or manual export)
2. Paste specs into Claude with this template:

```
Using these Pencil specs:
[PASTE SPECS HERE]

Generate pixel-perfect React components with:
- CSS variables for all design tokens
- Exact measurements from specs
- data-theme attribute for light/dark modes
- Semantic HTML structure
- No hardcoded colors or spacing
```

#### Path B: Pencil AI Agent → Refine
1. Use Pencil's built-in AI agent to generate code
2. Import generated code into Claude Code
3. Refine for pixel-perfect alignment

#### Path C: Manual Component Mapping
1. List components and their specs manually
2. Feed to Claude with structured format (JSON or YAML)
3. Generate with full spec validation

### Step 3: Three-Layer Validation

Every generated component gets validated at three levels:

#### Layer 1: Structural Validation
- **Component hierarchy** — Does the tree match Pencil structure?
- **Semantic HTML** — Is markup correct (buttons, links, inputs)?
- **Props API** — Do variant/size/state props exist as designed?

#### Layer 2: Visual Fidelity Validation
- **Typography** — Font family, size, line-height, weight match specs?
- **Color** — All brand colors use CSS variables? Contrast ≥ 4.5:1 (AA)?
- **Spacing** — All padding/margin align to 8px grid?
- **Alignment** — Flexbox/Grid layout matches visual flow?
- **Border radius** — Corners consistent with design system?

#### Layer 3: Pixel-Perfect Specs Validation
Compare generated code against original measurements:

```json
{
  "validations": [
    {
      "element": ".button.primary",
      "spec": { "height": 44, "padding": "12px 16px", "fontSize": 16 },
      "actual": "✓ matches spec",
      "status": "pass"
    }
  ]
}
```

### Step 4: Component Extraction & Reusability

Identify reusable components:

```markdown
## Button Component

**Usage:**
```jsx
<Button variant="primary" size="md" disabled={false}>
  Click me
</Button>
```

**Props:**
- `variant`: "primary" | "secondary" | "ghost" (required)
- `size`: "sm" | "md" | "lg" (default: "md")
- `disabled`: boolean (default: false)

**Specs:**
- Heights: sm=32px, md=44px, lg=56px
- Padding: 12px 16px (relative to typography)
- Font: Design system primary, 16px, weight 500
- Colors: Use CSS variables (--color-primary, etc)
```

### Step 5: Animation Standards (Critical for Web Apps)

**Every animation MUST follow these standards** to maintain consistency:

#### List & Collection Animations (UNIVERSAL PATTERN)
```typescript
{items.map((item, idx) => (
  <motion.div
    key={idx}
    initial={{ opacity: 0 }}
    animate={{ opacity: 1 }}
    transition={{ duration: 0.3, delay: idx * 0.05, ease: [0.25, 0.46, 0.45, 0.94] }}
  >
    {/* Content */}
  </motion.div>
))}
```

**Rules:**
- **Duration**: 0.3s (no variations)
- **Easing**: `[0.25, 0.46, 0.45, 0.94]` (cubic-bezier standard)
- **Stagger**: 50ms between items (`delay: idx * 0.05`)
- **Entry**: `opacity: 0 → 1` (fade only, NO transforms)
- **Container**: Wrap with `<AnimatePresence>` when list changes

#### Page Transitions (0.5s fade)
```typescript
<motion.div
  key={pathname}
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 0.5, ease: [0.25, 0.46, 0.45, 0.94] }}
>
  {children}
</motion.div>
```

**Rules:**
- **Duration**: ALWAYS 0.5s
- **Easing**: `[0.25, 0.46, 0.45, 0.94]` (cubic-bezier)
- **No exit animations** (prevents double fade)
- **Key change triggers animation** on route change

#### Bottom Sheet Standard
```typescript
<AnimatePresence>
  <motion.div
    initial={{ y: '100%' }}
    animate={{ y: 0, transition: { type: 'spring', damping: 30, stiffness: 300 } }}
    exit={{ y: '100%', transition: { duration: 0.2 } }}
  >
    {/* Content with staggered children */}
  </motion.div>
</AnimatePresence>
```

**Rules:**
- **Entry**: Spring physics (not linear fade)
- **Exit**: 0.2s slide down
- **Children**: Use `staggerChildren: 0.1` for reveal

### Step 6: Log Design Decisions & Rationale

Document **why** design choices were made, not just **what**:

```markdown
## Component: Button

### Decision
Used CSS modules + BEM naming for variant/size classes.

### Rationale
- Variants as class modifiers (primary, secondary) vs separate components
  - Easier to compose (one component, infinite combinations)
  - Smaller bundle size
- Responsive: sizes hardcoded to specific heights (no fluid sizing)
  - Button click targets need minimum size for accessibility

### Trade-offs
- Can't mix variant + size in same element (by design)
  - Could add compound variant if needed later

### Validation
✓ All spec values match exactly
✓ Colors match on light + dark themes
✓ 44px height passes WCAG touch target (minimum 44×44)
```

---

## Animation Anti-Patterns (FORBIDDEN)

These patterns MUST be avoided:

| Anti-Pattern | Why It Fails | Fix |
|---|---|---|
| **Custom bottom sheets** | Breaks consistency, hard to maintain | Use BottomSheet component |
| **Different easing per component** | Makes UI feel chaotic | Always use cubic-bezier `[0.25, 0.46, 0.45, 0.94]` |
| **Stagger delays other than `idx * 0.05`** | Inconsistent timing feels unpolished | Use 50ms stagger (5% of 1000ms) |
| **Spring physics on list items** | Bouncy lists feel cheap and slow animations down | Use fade only (opacity) |
| **Different durations per context** | Unpredictable feels broken | Use 0.3s for lists, 0.5s for pages |
| **Transform/y-axis on lists** | Causes layout shifts and repaints | Use opacity only |
| **Variants stored separately** | Hard to find/update animation logic | Use inline `initial`, `animate`, `exit` |
| **Fake progress bars** | Users feel deceived | Use honest, deterministic progress |

---

## Validation Checklist

After generating code, validate systematically:

### Structure
- [ ] Component names match Pencil specs
- [ ] Props align with design variations
- [ ] DOM hierarchy is semantic
- [ ] No prop drilling beyond 2 levels

### Visual Fidelity
- [ ] Typography: Font, size, weight, line-height match spec
- [ ] Colors: All using CSS variables, no hardcoded hex
- [ ] Spacing: All values align to 8px grid
- [ ] Alignment: Flexbox/Grid layout visually correct
- [ ] Border radius: Consistent with system

### Pixel-Perfect Specs
- [ ] Component dimensions (height, width) exact
- [ ] Padding/margin match spec values
- [ ] Gaps between child elements correct
- [ ] Responsive breakpoints implemented
- [ ] Dark/light mode variables working

### Animation (if applicable)
- [ ] List items use fade only (opacity: 0 → 1)
- [ ] Stagger delay is `idx * 0.05`
- [ ] Duration is 0.3s for lists, 0.5s for pages
- [ ] Easing is `[0.25, 0.46, 0.45, 0.94]`
- [ ] Page transitions have NO exit animation
- [ ] Bottom sheets use spring entry + slide exit

### Code Quality
- [ ] No inline styles (use CSS classes)
- [ ] No magic numbers (use variables)
- [ ] Accessibility: alt text, ARIA labels, contrast
- [ ] No console errors/warnings
- [ ] Builds without warnings

### Documentation
- [ ] Component API documented
- [ ] Props have JSDoc comments
- [ ] Design decisions logged
- [ ] Rationale for CSS patterns explained

---

## File Structure (Recommended)

```
my-project/
├── components/
│   ├── Button/
│   │   ├── Button.jsx
│   │   ├── Button.module.css
│   │   └── Button.stories.jsx (Storybook)
│   └── Card/
│       ├── Card.jsx
│       └── Card.module.css
├── design-system/
│   ├── tokens.css (all --color-, --spacing-, --font- vars)
│   └── global.css
├── docs/
│   ├── DESIGN_DECISIONS.md
│   └── COMPONENT_API.md
├── .claude/
│   └── CLAUDE.md (project context)
└── package.json
```

---

## Common Mistakes

| Mistake | Why It Fails | Fix |
|---------|-------------|---------|
| **No feedback on action** | Users don't know if their tap registered | Add immediate visual state change to every interactive element |
| **Overdesigning simple moments** | Complex animations slow down frequent actions | Reserve rich animation for infrequent, high-impact moments |
| **Ignoring edge cases** | Interaction breaks at zero, at max, or on double-tap | Map every state: empty, loading, partial, full, error, disabled |
| **Invisible triggers** | Users cannot discover functionality | Pair gesture triggers with a visible alternative |
| **Mode errors** | Same action produces different results | Make current mode visible; minimize number of modes |
| **Hardcoded pixel values** | Design system breaks with one change | Use CSS variables for everything (colors, spacing, fonts) |

---

## Quick Diagnostic Checklist

| Question | If No | Action |
|----------|-------|--------|
| Is there a clear, discoverable trigger? | Users cannot initiate the interaction | Add a visible control or affordance |
| Does the trigger show its current state? | Users cannot tell if it is on or off | Add distinct visual states |
| Are the rules simple and predictable? | Users are confused by what happened | Simplify rules; match platform conventions |
| Is there immediate feedback? | Users question whether their action worked | Add visual response within 100ms |
| Does feedback match the significance? | Small actions feel dramatic or vice versa | Scale feedback to match event importance |
| Are all values CSS variables? | Design token changes break the component | Replace all hardcoded values with variables |
| Is animation timing consistent? | Different durations feel chaotic | Use 0.3s lists, 0.5s pages, standard easing |

---

## Next Steps

1. **Extract specs** from Pencil (use export or manual list)
2. **Generate code** using appropriate path (A, B, or C)
3. **Validate** against checklist (all layers)
4. **Document** design decisions in DESIGN_DECISIONS.md
5. **Cross-check** visually against Pencil mockup
6. **Ship** when all validations pass ✓
