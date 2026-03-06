<img width="250" alt="p-logo-sm-cl-perfect" src="https://github.com/user-attachments/assets/a28111e3-29d1-446e-861a-4fabf6a47796" />

# Perfect - A Pencil to Claude Code Skill

Save time and pain by generating on-point applications directly from Pencil.dev designs using Claude Code.

<img height="600" alt="scene" src="https://github.com/user-attachments/assets/1ad333de-10ce-4f2b-8848-3608c842bc02" />

## Quick Start

### 1. Install

Copy to your Claude Code skills directory:
```bash
cp -r ~/.claude/skills/pencil-perfect SKILL.md
```

### 2. Connect Pencil

Make sure you have:
- [Pencil App](https://pencil.dev) installed and running
- [Pencil MCP](https://github.com/asl677/pencil-mcp-server) configured in Claude Code
- [Claude API key](https://console.anthropic.com)

### 3. Design with AI Agents

In Pencil:
1. Create your design (screens, components, layouts)
2. Use Pencil's AI agents (Cmd+K) to:
   - Generate component variations
   - Create responsive layouts
   - Extract design tokens
   - Refine the design

Save your `.pen` file when ready.

### 4. Build in Claude Code

In Claude Code, say:
```
Build a React app from my Pencil design [filename.pen]
```

The skill will:
- Extract components from your design
- Generate pixel-perfect React code
- Create CSS variables for theming
- Set up dark mode support
- Validate everything matches your design

---

## What You Get

- React components (JSX)
- CSS with variables (no hardcoded colors/spacing)
- Dark mode setup
- Responsive layouts
- Validation checklist
- Design documentation

---

## Workflow

```
1. Design in Pencil
         ↓
2. Use AI Agents
         ↓
3. Save .pen file
         ↓
4. Use Claude Code
         ↓
5. Get code + docs
```

---

## Example

**Pencil:** Design a Button with variants (primary, secondary) and sizes (small, medium, large)

**Claude Code:** "Build React components from this design"

**Output:**
- `Button.jsx` (all variants + sizes)
- `Button.css` (CSS variables)
- `DESIGN_DECISIONS.md` (why you made each choice)

---

## Tips

- Start with design tokens (colors, spacing, fonts) — everything else builds from these
- Use AI agents in Pencil to generate variations quickly
- Keep CSS variables for all values (no hardcoded `#colors` or `12px` padding)
- The skill validates your code matches the design exactly

---

Version 1.0 | Ready for production
