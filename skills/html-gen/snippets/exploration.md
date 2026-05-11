# Exploration & Planning Snippets

## 1. Option Comparison Table

Side-by-side comparison with pros/cons and rating.

```html
<div class="comparison-grid">
  <div class="option-card" style="--card-color: #e94560;">
    <div class="option-header">
      <h3>方案 A</h3>
      <div class="rating">★★★★☆</div>
    </div>
    <div class="option-body">
      <h4>优点</h4>
      <ul class="pros">
        <li>实现简单</li>
        <li>性能优秀</li>
      </ul>
      <h4>缺点</h4>
      <ul class="cons">
        <li>扩展性有限</li>
      </ul>
    </div>
    <div class="option-footer">
      <span class="tag">推荐</span>
      <span class="complexity">复杂度: 低</span>
    </div>
  </div>
  <!-- Repeat for other options -->
</div>

<style>
.comparison-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 20px;
  padding: 20px;
}
.option-card {
  background: var(--bg-card);
  border-radius: 12px;
  border-top: 4px solid var(--card-color);
  padding: 20px;
  transition: transform 0.2s;
}
.option-card:hover {
  transform: translateY(-4px);
}
.option-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}
.rating { color: #ffd700; }
.pros li { color: var(--success); }
.cons li { color: var(--error); }
.tag {
  background: var(--accent);
  color: white;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.85em;
}
</style>
```

## 2. Decision Matrix

Weighted scoring matrix with interactive sliders.

```html
<div class="decision-matrix">
  <table>
    <thead>
      <tr>
        <th>标准</th>
        <th>权重</th>
        <th>方案 A</th>
        <th>方案 B</th>
        <th>方案 C</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>性能</td>
        <td><input type="range" min="1" max="10" value="8" class="weight-slider"></td>
        <td><input type="number" min="1" max="10" value="9"></td>
        <td><input type="number" min="1" max="10" value="7"></td>
        <td><input type="number" min="1" max="10" value="6"></td>
      </tr>
      <!-- More rows -->
    </tbody>
    <tfoot>
      <tr>
        <td colspan="2"><strong>加权总分</strong></td>
        <td class="score" id="score-a">-</td>
        <td class="score" id="score-b">-</td>
        <td class="score" id="score-c">-</td>
      </tr>
    </tfoot>
  </table>
</div>

<script>
function calculateScores() {
  const rows = document.querySelectorAll('tbody tr');
  const scores = { a: 0, b: 0, c: 0, totalWeight: 0 };
  rows.forEach(row => {
    const weight = parseInt(row.querySelector('.weight-slider').value);
    const values = row.querySelectorAll('input[type="number"]');
    scores.a += weight * parseInt(values[0].value);
    scores.b += weight * parseInt(values[1].value);
    scores.c += weight * parseInt(values[2].value);
    scores.totalWeight += weight;
  });
  document.getElementById('score-a').textContent = (scores.a / scores.totalWeight).toFixed(1);
  document.getElementById('score-b').textContent = (scores.b / scores.totalWeight).toFixed(1);
  document.getElementById('score-c').textContent = (scores.c / scores.totalWeight).toFixed(1);
}
document.querySelectorAll('input').forEach(el => el.addEventListener('input', calculateScores));
calculateScores();
</script>
```

## 3. Multi-Path Exploration Tree

Collapsible tree showing different paths with trade-offs.

```html
<div class="exploration-tree">
  <div class="tree-node root">
    <div class="node-content">
      <span class="node-title">问题</span>
      <span class="node-desc">如何优化数据库查询？</span>
    </div>
    <div class="tree-branches">
      <div class="branch">
        <div class="branch-label">路径 A</div>
        <div class="tree-node">
          <div class="node-content">
            <span class="node-title">添加索引</span>
            <span class="node-desc">快速，但增加写入开销</span>
          </div>
        </div>
      </div>
      <div class="branch">
        <div class="branch-label">路径 B</div>
        <div class="tree-node">
          <div class="node-content">
            <span class="node-title">缓存层</span>
            <span class="node-desc">需要额外基础设施</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
```
