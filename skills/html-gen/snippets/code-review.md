# Code Review Snippets

## 1. Annotated PR View

PR with inline comments and annotations.

```html
<div class="pr-view">
  <div class="pr-header">
    <h1>feat: 添加用户认证模块</h1>
    <div class="pr-meta">
      <span class="author">@developer</span>
      <span class="branch">feature/auth → main</span>
      <span class="status approved">已批准</span>
    </div>
  </div>

  <div class="file-diff">
    <div class="file-header">
      <span class="filename">src/auth/middleware.js</span>
      <span class="changes">+42 -8</span>
    </div>
    <div class="diff-content">
      <div class="diff-line added">
        <span class="line-num">15</span>
        <span class="code">+ const verifyToken = async (req, res, next) => {</span>
        <div class="comment">
          <div class="comment-author">@reviewer</div>
          <div class="comment-body">建议添加错误处理中间件</div>
        </div>
      </div>
      <div class="diff-line removed">
        <span class="line-num">16</span>
        <span class="code">- const verify = (req, res, next) => {</span>
      </div>
    </div>
  </div>
</div>

<style>
.pr-view { max-width: 960px; margin: 0 auto; }
.pr-header { background: var(--bg-card); padding: 20px; border-radius: 8px; margin-bottom: 20px; }
.pr-meta { display: flex; gap: 16px; margin-top: 8px; color: var(--text-secondary); }
.status { padding: 4px 12px; border-radius: 20px; font-size: 0.85em; }
.status.approved { background: var(--success); color: white; }
.file-diff { background: var(--bg-secondary); border-radius: 8px; overflow: hidden; }
.file-header { background: var(--bg-card); padding: 12px 16px; display: flex; justify-content: space-between; }
.diff-line { display: flex; padding: 4px 16px; font-family: monospace; }
.diff-line.added { background: rgba(76, 175, 80, 0.15); }
.diff-line.removed { background: rgba(244, 67, 54, 0.15); }
.comment { margin: 8px 0 8px 40px; padding: 12px; background: var(--bg-card); border-radius: 6px; border-left: 3px solid var(--accent); }
</style>
```

## 2. Module Relationship Diagram

SVG-based module dependency graph.

```html
<div class="module-graph">
  <svg viewBox="0 0 600 400" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="10" refY="3.5" orient="auto">
        <polygon points="0 0, 10 3.5, 0 7" fill="#e94560"/>
      </marker>
    </defs>

    <!-- Modules -->
    <rect x="50" y="50" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="110" y="85" text-anchor="middle" fill="white">auth</text>

    <rect x="250" y="50" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="310" y="85" text-anchor="middle" fill="white">api</text>

    <rect x="150" y="200" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="210" y="235" text-anchor="middle" fill="white">database</text>

    <!-- Dependencies -->
    <line x1="170" y1="80" x2="250" y2="80" stroke="#e94560" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="310" y1="110" x2="210" y2="200" stroke="#e94560" stroke-width="2" marker-end="url(#arrowhead)"/>
  </svg>
</div>
```

## 3. Code Quality Heatmap

File-level quality metrics visualization.

```html
<div class="quality-heatmap">
  <h3>代码质量热力图</h3>
  <div class="heatmap-grid">
    <div class="heatmap-cell good" style="--score: 92;" data-file="src/utils.js" data-score="92">
      <span class="cell-name">utils.js</span>
      <span class="cell-score">92</span>
    </div>
    <div class="heatmap-cell warning" style="--score: 68;" data-file="src/api.js" data-score="68">
      <span class="cell-name">api.js</span>
      <span class="cell-score">68</span>
    </div>
    <div class="heatmap-cell danger" style="--score: 45;" data-file="src/legacy.js" data-score="45">
      <span class="cell-name">legacy.js</span>
      <span class="cell-score">45</span>
    </div>
  </div>
</div>

<style>
.heatmap-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(100px, 1fr)); gap: 8px; }
.heatmap-cell { padding: 12px; border-radius: 8px; text-align: center; cursor: pointer; transition: transform 0.2s; }
.heatmap-cell:hover { transform: scale(1.05); }
.heatmap-cell.good { background: rgba(76, 175, 80, 0.3); border: 1px solid var(--success); }
.heatmap-cell.warning { background: rgba(255, 152, 0, 0.3); border: 1px solid var(--warning); }
.heatmap-cell.danger { background: rgba(244, 67, 54, 0.3); border: 1px solid var(--error); }
.cell-name { display: block; font-weight: bold; }
.cell-score { font-size: 1.5em; }
</style>
```
