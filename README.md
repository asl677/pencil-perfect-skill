# Pencil-to-Code: Pixel-Perfect Design Workflow

## Overview

A comprehensive Claude skill for converting Pencil designs to production-ready, pixel-perfect code with automatic validation and design decision logging.

**What it does:**
- Extracts design specs from Pencil files/exports
- Generates pixel-perfect React/HTML code
- Validates component structure, visual fidelity, and measurements
- Extracts and documents reusable components
- Logs design decisions & rationale to your project docs

**Key features:**
- ✅ **Three-layer validation** (structure, visual fidelity, pixel-perfect specs)
- ✅ **CSS variable-first** — No hardcoded values
- ✅ **Mixed workflow support** — Works with Pencil exports, AI agent output, or manual specs
- ✅ **Design decision logging** — Track *why* you made design choices, not just *what*
- ✅ **Component API documentation** — Auto-generate for Storybook/teams

---

## Files Included

```
pencil-to-code-pixel-perfect/
├── SKILL.md                 # Main skill document (copy to your ~/.claude/skills/)
├── test-cases.json         # 6 test cases validating different workflows
├── test-1-output.md        # Example: Button component workflow (PASS ✓)
└── README.md               # This file
```

---

## Installation

### Option 1: Copy to Claude Skills Directory
```bash
cp -r pencil-to-code-pixel-perfect ~/.claude/skills/pencil-to-code-pixel-perfect
```

### Option 2: Use in Claude Code
The skill works in Claude Code CLI or Claude.ai. Just load the SKILL.md file and reference it in your workflow.

### Option 3: Marketplace Installation
If you upload this to a marketplace (obra, ananddtyagi, anthropics), others can install it via marketplace search.

---

## Quick Start Workflow

```
Prepare Design Specs
         ↓
   Generate Code
         ↓
   Validate Output
         ↓
  Document Decisions
```

---

### 1. Prepare Your Design Specs

**Option A: Export from Pencil**
```bash
# In Pencil, use Cmd/Ctrl + K to trigger AI agent
# Ask: "Export component specs as JSON"
# Copy output
```

**Option B: Manual Specs (JSON)**
```json
{
  "component": "Button",
  "variants": {
    "primary": { "bg": "#0f0d0a", "text": "#fefefe" },
    "secondary": { "bg": "transparent", "border": "1px solid #0f0d0a" }
  },
  "sizes": {
    "sm": { "height": 32, "padding": "8px 12px", "fontSize": 12 },
    "md": { "height": 44, "padding": "12px 16px", "fontSize": 16 }
  }
}
```

### 2. Generate Code

Prompt Claude Code with:
```
Using the pencil-to-code-pixel-perfect skill, generate pixel-perfect 
React component code from these Pencil specs:

[PASTE SPECS HERE]

Requirements:
- All measurements use CSS variables
- Validate all specs match exactly
- Document design decisions
```

### 3. Validate

The skill will:
- ✅ Check component structure (props, variants)
- ✅ Verify visual fidelity (colors, fonts, spacing)
- ✅ Cross-check pixel-perfect measurements
- ✅ Show validation results (pass/fail)

### 4. Document

The skill automatically generates:
- Component code (React JSX)
- CSS modules with variables
- Design decision log entry
- Validation checklist

---

## Workflow Examples

### Example 1: Pencil Export → Code → Validate

**Step 1: Export from Pencil**
```
User: "Here are my Button component specs from Pencil..."
[PASTE SPECS]
```

**Step 2: Generate Code**
```
Skill output:
✅ Button.jsx (React component)
✅ Button.module.css (CSS with variables)
✅ Validation results (all measurements match)
✅ Design decision log
```

**Step 3: Cross-check**
```
Visual comparison:
Left: Pencil mockup
Right: Generated code
Result: Pixel-perfect match ✓
```

---

### Example 2: Pencil AI Agent → Refine → Validate

**Step 1: Use Pencil's AI Agent**
```
User: "Pencil's AI generated this code, but it has hardcoded values"
[PASTE AI-GENERATED CODE]
```

**Step 2: Refine**
```
Skill identifies issues:
❌ Hardcoded colors (#0f0d0a)
❌ Hardcoded padding (16px)
❌ Missing CSS variables
```

**Step 3: Fix & Validate**
```
Skill output:
✅ Refactored to CSS variables
✅ Added component props (variant, size)
✅ Validation passes (all specs match)
✅ Design rationale documented
```

---

### Example 3: Design System with Multiple Components

**Step 1: Extract Design Tokens**
```
Colors: #0f0d0a, #fefefe, accent colors
Typography: DM Serif Display, font sizes 12-32px
Spacing: 8px grid (8, 16, 24, 32px)
Border radius: 4px, 8px, 12px
```

**Step 2: Generate Components**
```
Button → variants (primary, secondary) × sizes (sm, md, lg)
Card → padding, border radius, shadows
Typography → font scales, weights
```

**Step 3: Validate System-Wide**
```
✅ All spacing aligns to 8px grid
✅ All colors use CSS variables
✅ Typography scales match spec
✅ No hardcoded values anywhere
```

**Step 4: Document All Decisions**
```
DESIGN_DECISIONS.md:
- Why 8px grid (divisible, flexible, WCAG touch targets)
- Why CSS variables (theming, updates, consistency)
- Why Grid vs Flexbox for layouts (2D vs 1D)
- Light/dark mode implementation
```

---

## Validation Checklist

Copy this to your project. Check all boxes before shipping:

### Structure
- [ ] Component names match Pencil specs
- [ ] All variants are implemented
- [ ] All sizes are implemented
- [ ] Props API matches design
- [ ] DOM structure is semantic

### Visual Fidelity
- [ ] Font family correct
- [ ] Font sizes match spec
- [ ] Font weights match spec
- [ ] Colors use CSS variables (not hardcoded)
- [ ] Spacing aligns to grid
- [ ] Border radius matches spec
- [ ] Layout (Flexbox/Grid) matches visual flow

### Pixel-Perfect
- [ ] Component heights exact match
- [ ] Padding values exact match
- [ ] Margins exact match
- [ ] Gaps between children exact match
- [ ] Responsive breakpoints work
- [ ] Light mode correct
- [ ] Dark mode correct

### Code Quality
- [ ] No inline styles
- [ ] No magic numbers
- [ ] CSS variables everywhere
- [ ] JSDoc comments on props
- [ ] No console errors/warnings
- [ ] Builds without warnings

### Documentation
- [ ] Component API documented
- [ ] Design decisions logged
- [ ] Rationale for CSS patterns explained
- [ ] Code linked to design decisions

---

## Design Decision Log Template

Use this template for every significant design choice:

```markdown
## [Date] Component: [Name]

### Decision
[What did you choose? One sentence.]

### Rationale
[Why this over alternatives?]

### Alternatives Considered
- **Option A**: [Pros/cons]
- **Option B**: [Pros/cons]

### Implementation
[Code snippet]

### Trade-offs
[What's the cost?]

### Validation
[How did you verify it works?]

### Status
✓ Complete / ⏳ In progress / ❌ Blocked
```

---

## Example: Button Component

See `test-1-output.md` for a complete worked example including:
- ✅ Generated React component
- ✅ CSS modules with variables
- ✅ Design system tokens
- ✅ Layer 1-3 validation results
- ✅ Design decision log entry

This shows the full workflow in action.

---

## Tips for Success

### 1. Start with Design Tokens
Extract spacing, typography, colors **first**. Everything else builds from these.

```css
/* Good: Define tokens at system level */
:root {
  --spacing-1: 8px;
  --spacing-2: 16px;
  --font-serif: 'DM Serif Display', serif;
}

/* Bad: Tokens buried in component files */
.button { padding: 12px 16px; }
```

### 2. Use CSS Variables Everywhere
No hardcoded values. Ever.

```css
/* Good */
padding: var(--spacing-3);
color: var(--color-primary);

/* Bad */
padding: 12px;
color: #0f0d0a;
```

### 3. Document Trade-offs
Not just "what," but "why." Include alternatives you rejected.

```markdown
❌ Rejected Flexbox (1D layout, harder to center vertically without hacks)
✅ Chose Grid (2D layout, automatic alignment, simpler responsive)
```

### 4. Validate Before Shipping
Run the checklist above. One spec mismatch breaks "pixel-perfect."

### 5. Version Control Design Docs
Keep `DESIGN_DECISIONS.md` in git alongside code. Link commits to decisions.

```markdown
## Button Component

### Status
✓ Complete (commit abc123de)
```

---

## Test Cases

The skill includes 6 test cases covering different workflows:

1. **Button Generation** — Generate pixel-perfect component from specs
2. **Mixed Workflow** — Refine Pencil AI output
3. **Validation Mismatch** — Catch and fix measurement errors
4. **Design Decision Documentation** — Log design rationale
5. **Dark Mode Validation** — Light/dark theme setup & validation
6. **Component Extraction** — Identify reusable patterns across screens

See `test-cases.json` for details.

---

## FAQ

**Q: Do I need to use Pencil's AI agent?**
A: No. The skill works with manual specs, Pencil exports, or AI-generated code. Mix and match.

**Q: What if my Pencil specs don't perfectly align to a grid?**
A: The skill will flag misalignment in validation. You can either:
- Round to nearest grid value (4px, 8px, 16px, etc)
- Add the "off-grid" value to design tokens and document the decision
- Go back to Pencil and adjust the spec

**Q: How do I handle variants that don't fit the Props pattern?**
A: Use the "Compound Variant" pattern:
```jsx
<Button variant="primary" size="md" state="hover">
```
Or separate components if truly distinct:
```jsx
<PrimaryButton /> vs <SecondaryButton />
```

**Q: What if generated code doesn't match my Pencil design perfectly?**
A: The skill includes a validation layer to catch mismatches. Common causes:
- Hardcoded values (should be CSS variables)
- Spacing not aligning to grid
- Font size/weight mismatch
- Color not using theme variable

Run validation to identify the issue, then regenerate.

**Q: How do I export the design decision log?**
A: Keep `DESIGN_DECISIONS.md` in your project root. It's version-controlled with code.
You can:
- Share via GitHub
- Convert to PDF for stakeholders
- Link in pull request descriptions
- Reference in code reviews

---

## Support & Feedback

### To improve this skill:
1. Try it on a real project
2. Note what works and what doesn't
3. Run the test cases — do they pass?
4. Share feedback on triggering (when should it activate?)
5. Suggest additional validations or design patterns

### Common issues:
- **Skill not triggering?** — Add more explicit keywords to your prompt (use "Pencil," "design specs," "component")
- **Validation failing?** — Check that all values are grid-aligned (8px multiples)
- **Design decision doc too long?** — Archive old decisions to separate section

---

## Next Steps

1. **Copy SKILL.md** to `~/.claude/skills/pencil-to-code-pixel-perfect/`
2. **Try a test case** — Use test-1 (Button) as a template
3. **Apply to your project** — Start with one component (Button, Card, etc)
4. **Document decisions** — Create DESIGN_DECISIONS.md in your project
5. **Iterate** — Refine the skill based on feedback

---

## File Structure (Recommended for Your Project)

```
my-project/
├── components/
│   ├── Button/
│   │   ├── Button.jsx
│   │   ├── Button.module.css
│   │   └── Button.stories.jsx
│   ├── Card/
│   ├── Typography/
├── design-system/
│   ├── tokens.css          # All --color-, --spacing-, --font- vars
│   └── global.css
├── docs/
│   ├── DESIGN_DECISIONS.md # Decision log (copy template from skill)
│   └── COMPONENT_API.md    # Auto-generated component APIs
├── .claude/
│   └── CLAUDE.md           # Project context for Claude Code
└── package.json
```

---

## Version

**Skill Version:** 1.0  
**Created:** 2026-03-04  
**Status:** Ready for production use

---

Enjoy building pixel-perfect designs with Pencil and Claude! 🎨✨
