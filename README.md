# Claude Code Skills

Claude Code skills repository. `html-gen` skill automatically generates self-contained HTML files with interactive components (drag-drop, charts, forms) across 9 categories: exploration, code review, design, prototyping, charts, presentations, research, reports, and custom editors.

## Why HTML Instead of Markdown?

> "Motion and interaction can't be described, only felt."

This skill is inspired by the idea that [HTML as an output format is extraordinarily effective](https://thariqs.github.io/html-effectiveness/). When AI agents generate documents, they typically default to Markdown — a format you'll skim. HTML turns those into documents you'll actually read.

**Markdown** is great for text. But when you need:
- Side-by-side comparisons
- Interactive diagrams
- Collapsible sections
- Drag-and-drop interfaces
- Real-time previews
- Visual timelines

...Markdown falls short. HTML delivers.

## Installation

### Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- Git (optional, for cloning)

### Method 1: Clone the entire repository

```bash
git clone https://github.com/YOUR_USERNAME/skills.git ~/.claude/skills/skills
```

This installs all skills in the repository. The `html-gen` skill will be available at `~/.claude/skills/skills/html-gen/`.

### Method 2: Copy only html-gen

```bash
# Clone to a temporary location
git clone https://github.com/YOUR_USERNAME/skills.git /tmp/skills

# Copy just the html-gen skill
cp -r /tmp/skills/html-gen ~/.claude/skills/

# Clean up
rm -rf /tmp/skills
```

### Method 3: Download ZIP

1. Go to the [repository page](https://github.com/YOUR_USERNAME/skills)
2. Click "Code" → "Download ZIP"
3. Extract the ZIP file
4. Copy the `html-gen` folder to `~/.claude/skills/`

### Verify Installation

After installation, restart Claude Code and check if the skill is available:

```
/html-gen
```

Or simply describe a task that would benefit from HTML output, and the skill will trigger automatically.

### Directory Structure

Your Claude Code skills directory should look like:

```
~/.claude/skills/
├── html-gen/           <- The skill you just installed
│   ├── SKILL.md
│   ├── snippets/
│   └── ...
└── (other skills)
```

## The html-gen Skill

### When It Triggers

The skill automatically detects the appropriate category based on your request:

| Category | What It Does | Example Prompts |
|----------|--------------|-----------------|
| **Exploration & Planning** | Compare options, evaluate approaches | "对比三种数据库方案" |
| **Code Review** | Annotated PRs, module diagrams | "帮我review这个PR" |
| **Design** | Color palettes, component variants | "生成设计系统的色板" |
| **Prototyping** | Interactive prototypes, animation tools | "做一个可点击的流程演示" |
| **Charts & Illustrations** | SVG diagrams, flowcharts, graphs | "画一个架构图" |
| **Presentations** | Keyboard-driven slides | "做一个技术分享的slides" |
| **Research & Learning** | Interactive explanations, tutorials | "解释一下React的reconciliation" |
| **Reports** | Weekly reports, incident timelines | "生成本周的周报" |
| **Custom Editors** | Kanban boards, feature toggles, prompt tuners | "做一个任务看板" |

### Features

- **Self-contained files** — Single HTML with inline CSS/JS, works offline
- **CDN libraries** — Uses Chart.js, SortableJS, Tailwind when needed
- **4 built-in themes** — Dark (default), Light, Vibrant, Minimal
- **Smart interaction** — Editors get drag-drop/forms, reports stay static
- **Export functionality** — Custom editors include export to JSON/CSV/text
- **Responsive design** — Desktop-first, mobile when straightforward
- **User preferences** — Saves to `.html-gen-config.json`

### Usage

Just describe what you need:

```
"帮我做一个本周的周报"
"生成一个API对比的HTML页面"
"做一个功能开关编辑器"
"画一个系统架构图"
```

The skill will:
1. Detect the category
2. Ask about special requirements (if ambiguous)
3. Generate the HTML file
4. Place it alongside related project files

### Configuration

Create `.html-gen-config.json` in your project root:

```json
{
  "default_theme": "dark",
  "default_interaction": "auto",
  "responsive": "auto",
  "use_cdn": true,
  "export_editors": true
}
```

### File Structure

```
html-gen/
├── SKILL.md                    # Skill definition and rules
├── config/
│   └── default-config.json     # Default themes and category settings
├── references/
│   └── example-index.html      # Index page template
└── snippets/                   # Component libraries
    ├── exploration.md          # Comparison tables, decision matrices
    ├── code-review.md          # PR views, module diagrams
    ├── design.md               # Color palettes, component showcases
    ├── prototyping.md          # Kanban boards, flow builders
    ├── charts.md               # SVG flowcharts, pie charts
    ├── presentations.md        # Slide decks, code highlights
    ├── research.md             # Concept explainers, tabbed content
    ├── reports.md              # Weekly reports, incident timelines
    └── editors.md              # Feature toggles, prompt tuners
```

## Design Philosophy

### 1. Output Should Be Felt, Not Just Read

A kanban board you can drag. A color palette you can click to copy. A flowchart you can navigate. These experiences can't be conveyed in plain text.

### 2. Single File, Zero Setup

Every generated HTML is self-contained. Open it in any browser. No build tools, no npm install, no configuration. It just works.

### 3. Smart Defaults, Full Control

The skill makes good decisions by default — dark theme for dashboards, static layout for reports, interactive mode for editors. But you can override everything.

### 4. Composable Components

The snippet library provides battle-tested components that combine flexibly. A weekly report might use the timeline component. A code review might use the heatmap component. Mix and match.

## Contributing

1. Fork this repository
2. Create your skill in a new directory
3. Submit a PR with a clear description

## License

MIT

## Acknowledgments

Inspired by [HTML Effectiveness](https://thariqs.github.io/html-effectiveness/) — a demonstration of why HTML is an extraordinarily effective output format for AI agents.
