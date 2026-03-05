![Prfct Logo](./logo.png)

# Pencil-Perfect: Design in Pencil, Build in Claude Code

Design with Pencil AI agents, export `.pen` file, run in Claude Code, get pixel-perfect React app, edit back and forth.

---

## Quick Start

### 1. Design in Pencil
Create your design using Pencil's AI agent. Export as `.pen` file.

### 2. Run in Claude Code
Open Claude Code and say:
```
Use pencil-perfect skill to build React app from mydesign.pen
```

### 3. Get React App
Pixel-perfect React components with CSS variables, dark mode, responsive layouts.

### 4. Edit & Iterate
Update design in Pencil, sync changes in Claude Code.

---

## What the Skill Does

**Build from Pencil file:**
- Parse `.pen` specs (components, colors, spacing, fonts)
- Generate React components with TypeScript
- Create CSS modules with variables
- Set up dark mode and responsive breakpoints
- Generate validation checklist
- Document design decisions

**Update from changes:**
- Detect changes in Pencil specs
- Regenerate only modified components
- Sync CSS variables
- Update validation and docs

---

## What You Get

- Pixel-perfect React components
- CSS variables for theming
- Dark mode support
- Responsive layouts
- Validation checklist
- Design decision documentation

---

## Troubleshooting

**"Claude Code can't find the .pen file"**
- Make sure the `.pen` file is in your project root
- Use the exact filename in the command

**"Generated components don't match Pencil design"**
- Run validation to compare specs vs. generated code
- Check that all measurements are on 8px grid in Pencil
- Ensure colors and fonts are defined as variables

**"Dark mode not working"**
- Verify `data-theme="dark"` attribute is set on HTML element
- Check that CSS variables are defined in `[data-theme="dark"]` selector

**"Responsive layout broken on mobile"**
- Check inferred breakpoints match your design
- Test component at 480px, 768px, 1200px widths

**"Need to update after Pencil changes"**
- Say: "pencil-perfect: update from mydesign.pen"
- Only modified components will regenerate

---

## Resources

- [Pencil Design Tool](https://pencilapp.io)
- [Anthropic Skills Documentation](https://anthropic.com/docs/skills)
- [Claude Code Guide](https://claude.com/docs/claude-code)

---

## Commands in Claude Code

```
/pencil-perfect Build React app from mydesign.pen
/pencil-perfect Update components from mydesign.pen
/pencil-perfect Validate mydesign.pen against code
/pencil-perfect Generate DESIGN_DECISIONS.md
```

---

Built by Prfct | Part of agentskills
