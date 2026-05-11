# Research & Learning Snippets

## 1. Interactive Concept Explanation

Expandable sections with visual aids.

```html
<div class="concept-explainer">
  <h2>React Reconciliation 算法</h2>

  <div class="concept-section">
    <div class="section-header" onclick="toggleSection(this)">
      <h3>核心概念</h3>
      <span class="toggle-icon">+</span>
    </div>
    <div class="section-content hidden">
      <p>Reconciliation 是 React 用来比较两棵 Virtual DOM 树差异的算法。</p>
      <div class="visual-aid">
        <div class="tree before">
          <h4>更新前</h4>
          <div class="node">App</div>
          <div class="node child">Header</div>
          <div class="node child">Content</div>
        </div>
        <div class="arrow">→</div>
        <div class="tree after">
          <h4>更新后</h4>
          <div class="node">App</div>
          <div class="node child">Header</div>
          <div class="node child modified">Content*</div>
        </div>
      </div>
    </div>
  </div>

  <div class="concept-section">
    <div class="section-header" onclick="toggleSection(this)">
      <h3>Key 的作用</h3>
      <span class="toggle-icon">+</span>
    </div>
    <div class="section-content hidden">
      <p>Key 帮助 React 识别哪些元素发生了变化...</p>
    </div>
  </div>
</div>

<script>
function toggleSection(header) {
  const content = header.nextElementSibling;
  const icon = header.querySelector('.toggle-icon');
  content.classList.toggle('hidden');
  icon.textContent = content.classList.contains('hidden') ? '+' : '-';
}
</script>

<style>
.concept-section { margin: 16px 0; border: 1px solid var(--border); border-radius: 8px; overflow: hidden; }
.section-header { padding: 16px; background: var(--bg-card); cursor: pointer; display: flex; justify-content: space-between; align-items: center; }
.section-content { padding: 20px; }
.hidden { display: none; }
.visual-aid { display: flex; gap: 20px; align-items: center; justify-content: center; margin: 20px 0; }
.tree { text-align: center; }
.node { background: var(--bg-card); padding: 8px 16px; border-radius: 6px; margin: 4px; }
.node.child { margin-left: 20px; }
.node.modified { border: 2px solid var(--accent); }
.arrow { font-size: 2em; color: var(--accent); }
</style>
```

## 2. Technical Deep-Dive with Tabs

Multi-tab content organization.

```html
<div class="deep-dive">
  <h2>JWT 认证详解</h2>

  <div class="tabs">
    <button class="tab active" onclick="showTab('structure')">结构</button>
    <button class="tab" onclick="showTab('flow')">流程</button>
    <button class="tab" onclick="showTab('security')">安全</button>
  </div>

  <div class="tab-content" id="structure">
    <h3>JWT 的三部分</h3>
    <div class="jwt-parts">
      <div class="jwt-part header">
        <h4>Header</h4>
        <code>{"alg": "HS256", "typ": "JWT"}</code>
      </div>
      <div class="jwt-part payload">
        <h4>Payload</h4>
        <code>{"sub": "123", "name": "John"}</code>
      </div>
      <div class="jwt-part signature">
        <h4>Signature</h4>
        <code>HMACSHA256(...)</code>
      </div>
    </div>
  </div>

  <div class="tab-content hidden" id="flow">
    <p>认证流程说明...</p>
  </div>

  <div class="tab-content hidden" id="security">
    <p>安全注意事项...</p>
  </div>
</div>

<script>
function showTab(tabId) {
  document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
  document.querySelectorAll('.tab').forEach(el => el.classList.remove('active'));
  document.getElementById(tabId).classList.remove('hidden');
  event.target.classList.add('active');
}
</script>

<style>
.tabs { display: flex; gap: 4px; margin-bottom: 20px; }
.tab { padding: 10px 20px; background: var(--bg-secondary); border: none; color: var(--text-secondary); cursor: pointer; border-radius: 8px 8px 0 0; }
.tab.active { background: var(--bg-card); color: var(--text-primary); }
.jwt-parts { display: flex; gap: 12px; flex-wrap: wrap; }
.jwt-part { flex: 1; min-width: 200px; padding: 16px; background: var(--bg-card); border-radius: 8px; }
.jwt-part.header { border-top: 3px solid #e94560; }
.jwt-part.payload { border-top: 3px solid #0f3460; }
.jwt-part.signature { border-top: 3px solid #4caf50; }
</style>
```
