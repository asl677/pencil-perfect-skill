![Prfct Logo](./logo.png)

# Pencil-Perfect: Design in Pencil, Build in Claude Code

Design with Pencil AI agents → Export `.pen` file → Run in Claude Code → Get pixel-perfect React app → Edit back and forth.

---

## Quick Start

### 1. Design in Pencil
Use Pencil's AI agent to design your components:
- Create frames, buttons, cards, layouts
- Define colors, spacing, typography
- Export as `.pen` file

### 2. Export to Claude Code
1. Get your `.pen` file (e.g., `mydesign.pen`)
2. Open Claude Code in your project
3. Say: **"Use pencil-perfect skill to build this React app from mydesign.pen"**

### 3. Claude Code Builds Your App
The skill:
- Reads your `.pen` file specs
- Generates pixel-perfect React components
- Creates CSS variables for colors/spacing
- Sets up component library with validation

### 4. Edit & Iterate
- **In Pencil**: Adjust design, update specs
- **In Claude Code**: Say "pencil-perfect: update from mydesign.pen"
- Changes sync automatically

---

## What Pencil-Perfect Does

### When you say "build from mydesign.pen":

1. **Parse Pencil file** — Extract components, colors, spacing, typography specs
2. **Generate React components** — TSX files with props, variants, sizes
3. **Create CSS modules** — Pixel-perfect styling, no hardcoded values
4. **Set up design tokens** — CSS variables for colors, spacing, fonts
5. **Add dark mode** — `data-theme` attribute + variable overrides
6. **Build component library** — Organized folder structure, Storybook-ready
7. **Generate validation** — Checklist of specs vs. generated code
8. **Document decisions** — Design rationale, trade-offs, implementation notes
9. **Set up responsive** — Mobile, tablet, desktop breakpoints inferred from design
10. **Create index files** — Export all components, ready to import

### When you say "update from mydesign.pen":

1. **Detect changes** — Compare old Pencil specs vs. new specs
2. **Update components** — Only modified components regenerated
3. **Sync CSS variables** — New colors/spacing immediately available
4. **Refresh validation** — Re-check all specs
5. **Update docs** — Design decisions log updated

---

## What You Get

✅ Pixel-perfect React components
✅ CSS variables for theming
✅ Dark mode ready
✅ Responsive layouts
✅ Validation checklist
✅ Design decision docs

---

## Commands in Claude Code

**Build from Pencil file:**
```
/pencil-perfect Build React app from mydesign.pen
```

**Update existing app:**
```
/pencil-perfect Update components from mydesign.pen
```

**Validate specs:**
```
/pencil-perfect Validate mydesign.pen against generated code
```

**Document decisions:**
```
/pencil-perfect Generate DESIGN_DECISIONS.md for this project
```

---

## Workflow Example

```
Pencil (design)
    ↓ export myapp.pen
Claude Code (build)
    ↓ run skill
React App (generated)
    ↓ iterate
Edit in Pencil
    ↓ update specs
Claude Code
    ↓ sync changes
React App (updated)
```

---

## Install to Claude Code

1. Clone this repo:
   ```bash
   git clone https://github.com/asl677/pencil-perfect-skill
   cd pencil-perfect-skill
   ```

2. In Claude Code, add to your settings:
   ```json
   {
     "enabledPlugins": {
       "pencil-perfect-skill": true
     }
   }
   ```

3. Restart Claude Code

Now you can use `/pencil-perfect` commands in any project.

---

## What Pencil-Perfect Does

- **Extracts specs** from your `.pen` file (components, colors, spacing, typography)
- **Generates React code** that matches exactly (no guessing)
- **Creates CSS variables** for theming and dark mode
- **Sets up validation** so everything stays in sync
- **Documents decisions** so your team understands the system

---

## Made with ✓ for teams that design in Pencil

Built by [Prfct](https://prfct.com) | Part of [agentskills](https://agentskills.io)
