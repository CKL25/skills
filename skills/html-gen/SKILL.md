---
name: html-gen
description: "Generate rich, interactive HTML output instead of plain Markdown. Use this skill when the user asks to: create reports, dashboards, comparisons, timelines, flowcharts, kanban boards, design palettes, code review views, presentations, or any visual/interactive deliverable. Also trigger when the task would benefit from interactive elements (drag-drop, sliders, tabs, collapsible sections), visual layouts (side-by-side comparisons, color swatches, SVG diagrams), or structured presentations (weekly reports, incident timelines, PR summaries). Covers 9 categories: exploration & planning, code review, design, prototyping, charts & illustrations, presentations, research & learning, reports, and custom editors. If the user mentions 'HTML output', 'rich format', 'interactive report', 'visual comparison', or asks for something that would be better as a browsable page than plain text, use this skill."
---

# HTML Generator (html-gen)

Generate self-contained HTML files as rich alternatives to Markdown output.

## When to Use

Use HTML instead of Markdown when the output benefits from:
- **Visual layout**: side-by-side comparisons, grids, cards
- **Interactivity**: collapsible sections, tabs, drag-drop, sliders
- **Rich media**: SVG diagrams, color palettes, animated timelines
- **Structured navigation**: table of contents, anchor links, multi-tab views

## Before Generating: Ask About Special Requirements

Before generating any HTML, ask the user:

> "对于 [类别名称]，你有没有特殊要求？比如：
> - 配色/主题偏好（暗色、亮色、自定义颜色）
> - 特定的数据或内容需要展示
> - 是否需要响应式/移动端适配
> - 是否需要导出功能
> - 其他自定义需求"

Skip this question if:
- User explicitly specifies requirements in their request
- The task is obviously simple (e.g., "just show me a color palette")
- User has already expressed a preference (e.g., "make it dark theme")

## Category Detection

Determine the category based on the user's request:

| Category | Triggers | Examples |
|----------|----------|----------|
| **Exploration & Planning** | compare options, evaluate approaches, plan implementation | "对比三种方案的优劣" |
| **Code Review** | review PR, analyze code, show relationships | "帮我review这个PR" |
| **Design** | color palette, component variants, design system | "生成设计系统的色板" |
| **Prototyping** | animation, interaction flow, clickable prototype | "做一个可点击的流程演示" |
| **Charts & Illustrations** | diagram, flowchart, SVG chart, visualization | "画一个架构图" |
| **Presentations** | slides, deck, presentation | "做一个技术分享的slides" |
| **Research & Learning** | explain concept, technical deep-dive, tutorial | "解释一下React的reconciliation" |
| **Reports** | weekly report, incident timeline, status update | "生成本周的周报" |
| **Custom Editors** | kanban board, feature toggle, prompt tuner | "做一个任务看板" |

## Interaction Level by Category

| Category | Default Interaction Level |
|----------|---------------------------|
| Exploration & Planning | Static with collapsible sections |
| Code Review | Static with annotations |
| Design | Static showcase |
| **Prototyping** | **Interactive** (draggable, clickable) |
| Charts & Illustrations | Static SVG (interactive if user requests) |
| Presentations | Keyboard-driven slides |
| Research & Learning | Interactive explanations |
| Reports | Static with navigation |
| **Custom Editors** | **Interactive** (drag-drop, forms, real-time preview) |

For ambiguous cases, ask the user:
> "这个内容需要交互功能吗？比如可以拖拽、点击展开、实时编辑等？还是纯静态展示就够了？"

## Technical Constraints

### Default: Single File + CDN
- One `.html` file with inline CSS and JS
- Use CDN libraries when needed:
  ```html
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/sortablejs@latest/Sortable.min.js"></script>
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
  ```
- Works offline? No, but quality is higher

### If User Specifies:
- "纯HTML" / "离线可用" → All inline, no CDN
- "可以用任何库" → Full CDN freedom
- Custom constraint → Follow user's instruction

## File Placement

Default: Place HTML files alongside related project files.
- Code review → `./reviews/` or alongside the PR
- Weekly report → `./docs/` or `./reports/`
- Design → `./design/` or alongside design assets

If user specifies a path, use that instead.

## File Naming

- User specifies name → Use it
- Auto-generate: descriptive, kebab-case
  - `api-comparison.html`
  - `weekly-report-2024-05.html`
  - `component-palette.html`

## Export Functionality

**Custom Editors** (kanban, toggles, prompt tuner) MUST include export:
- Export to JSON/CSV/text
- Button in the UI that triggers download

**Other categories**: No export needed unless user requests.

## Visual Style

### Default Theme: Modern Dark
```css
:root {
  --bg-primary: #1a1a2e;
  --bg-secondary: #16213e;
  --bg-card: #0f3460;
  --text-primary: #e4e4e4;
  --text-secondary: #a0a0a0;
  --accent: #e94560;
  --accent-secondary: #0f3460;
  --border: #2a2a4a;
  --success: #4caf50;
  --warning: #ff9800;
  --error: #f44336;
}
```

### Alternative Themes (user can request):
- **Light**: Clean, professional, white background
- **Vibrant**: Colorful, playful, good for presentations
- **Minimal**: Black and white, focus on content

User can specify: "用亮色主题" / "暗色风格" / "简洁风格"

## Responsive Design

Default: Desktop-first.
- Make it responsive when:
  - User explicitly requests
  - Implementation is straightforward (simple layouts, no complex drag-drop)
  - The content is suitable for mobile (reports, timelines)
- Skip responsive when:
  - Complex interactions (kanban drag-drop, prototype builders)
  - Dense data tables
  - User specifies "desktop only"

## Index Page

Generate an `index.html` when:
- User asks for it
- Multiple HTML files exist and user wants to organize them

The index page should:
- List all generated HTML files
- Group by category
- Show brief descriptions
- Link to each file

## Reference Files

For component snippets and templates, read the relevant file:
- `snippets/exploration.md` - Comparison tables, option matrices
- `snippets/code-review.md` - PR views, code annotations
- `snippets/design.md` - Color palettes, component showcases
- `snippets/prototyping.md` - Interactive prototypes, animation tools
- `snippets/charts.md` - SVG diagrams, flowcharts
- `snippets/presentations.md` - Slide decks, keyboard navigation
- `snippets/research.md` - Technical explanations, tutorials
- `snippets/reports.md` - Timelines, weekly reports, status updates
- `snippets/editors.md` - Kanban boards, feature toggles, prompt tuners

## User Preferences

Load user preferences from `.html-gen-config.json` in the project root:

```json
{
  "default_theme": "dark",
  "default_interaction": "auto",
  "responsive": "auto",
  "use_cdn": true,
  "export_editors": true
}
```

If the file doesn't exist, use defaults above. Create it if user modifies preferences.
