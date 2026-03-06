<img width="250" alt="p-logo-sm-cl-perfect" src="https://github.com/user-attachments/assets/a28111e3-29d1-446e-861a-4fabf6a47796" />

# Perfect - A Pencil to Claude Code Skill

Save time and pain by generating on-point applications directly from Pencil.dev designs using Claude Code.

<img height="600" alt="scene" src="https://github.com/user-attachments/assets/1ad333de-10ce-4f2b-8848-3608c842bc02" />

## Prerequisites

Before installing, make sure you have:

- **[Claude Code CLI](https://github.com/anthropics/claude-code)** installed
- **[Node.js 18+](https://nodejs.org/)** installed
- **[Pencil App](https://pencil.dev)** downloaded
- **[Claude API key](https://console.anthropic.com)** from Anthropic

---

## Installation

### Step 1: Copy to Claude Code Skills Directory

```bash
cp -r ~/.claude/skills/pencil-perfect SKILL.md
```

Or manually clone:
```bash
git clone https://github.com/asl677/pencil-perfect-skill.git ~/.claude/skills/pencil-perfect
cd ~/.claude/skills/pencil-perfect && npm install
```

### Step 2: Verify Installation

In Claude Code, run:
```
/plugin list
```

You should see `pencil-perfect` in the list of available skills.

### Step 3 (Optional): Install from Marketplace

```
/plugin install pencil-perfect@ananddtyagi/cc-marketplace
```

---

## Quick Start

### 1. Prerequisites

Make sure you have installed the skill (see Installation section above).

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

## How to Use

### Trigger the Skill

In Claude Code, mention any of these:
- "Build from my Pencil design"
- "Generate React code from this .pen file"
- "Convert Pencil to code"
- "Create components from my design"

Or use the slash command:
```
/skills pencil-perfect
```

### Example Commands

**Basic:** Generate components from a design file
```
Build a React app from button-design.pen
```

**With specs:** Provide design specs if you don't have a .pen file
```
Generate a Button component with:
- Primary variant: blue background
- Secondary variant: transparent with border
- Sizes: small (32px), medium (44px), large (48px)
```

**Refine:** Fix hardcoded values in existing code
```
This React Button has hardcoded colors and padding.
Convert to CSS variables using design tokens.
```

---

## Troubleshooting

**"Skill not triggering?"**
- Use explicit keywords: "Pencil," "design," ".pen file," "component"
- Try: `Build from my Pencil design myfile.pen`

**"Generated code doesn't match my design"**
- Make sure all colors/spacing in Pencil are exact values
- Align measurements to 8px grid
- Check fonts and font sizes match exactly

**"Dark mode not working"**
- Verify CSS variables are defined for both light and dark themes
- Check that `data-theme="dark"` is set on the HTML root element

**"Missing CSS variables"**
- Generated code should use `var(--color-primary)` not hardcoded `#colors`
- If hardcoded, ask: "Convert all hardcoded values to CSS variables"

**"Responsive layout broken"**
- Test at 480px (mobile), 768px (tablet), 1200px (desktop)
- Check that grid/flexbox layouts adapt properly

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
