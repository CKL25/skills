# Custom Editors Snippets

## 1. Feature Toggle Editor

Toggle switches with environment config and export.

```html
<div class="toggle-editor">
  <h2>功能开关编辑器</h2>

  <div class="toggle-list">
    <div class="toggle-item">
      <div class="toggle-info">
        <h3>new-auth-flow</h3>
        <p>新版认证流程，支持 OAuth2.0</p>
      </div>
      <div class="toggle-envs">
        <label class="env-toggle">
          <span>Dev</span>
          <input type="checkbox" checked data-env="dev" data-flag="new-auth-flow">
          <span class="slider"></span>
        </label>
        <label class="env-toggle">
          <span>Staging</span>
          <input type="checkbox" data-env="staging" data-flag="new-auth-flow">
          <span class="slider"></span>
        </label>
        <label class="env-toggle">
          <span>Prod</span>
          <input type="checkbox" data-env="prod" data-flag="new-auth-flow">
          <span class="slider"></span>
        </label>
      </div>
    </div>
  </div>

  <div class="editor-actions">
    <button onclick="exportConfig()">导出配置</button>
    <button onclick="importConfig()">导入配置</button>
  </div>
</div>

<script>
function exportConfig() {
  const config = {};
  document.querySelectorAll('.toggle-item').forEach(item => {
    const flag = item.querySelector('h3').textContent;
    config[flag] = {};
    item.querySelectorAll('input[type="checkbox"]').forEach(cb => {
      config[flag][cb.dataset.env] = cb.checked;
    });
  });
  const blob = new Blob([JSON.stringify(config, null, 2)], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'feature-toggles.json';
  a.click();
}
</script>

<style>
.toggle-item { display: flex; justify-content: space-between; align-items: center; padding: 16px; background: var(--bg-card); border-radius: 8px; margin-bottom: 8px; }
.toggle-envs { display: flex; gap: 16px; }
.env-toggle { display: flex; align-items: center; gap: 8px; cursor: pointer; }
.env-toggle input { display: none; }
.slider { width: 44px; height: 24px; background: var(--bg-secondary); border-radius: 12px; position: relative; transition: background 0.3s; }
.slider::after { content: ''; position: absolute; width: 20px; height: 20px; background: white; border-radius: 50%; top: 2px; left: 2px; transition: transform 0.3s; }
.env-toggle input:checked + .slider { background: var(--success); }
.env-toggle input:checked + .slider::after { transform: translateX(20px); }
.editor-actions { margin-top: 20px; display: flex; gap: 12px; }
.editor-actions button { padding: 10px 20px; background: var(--accent); color: white; border: none; border-radius: 6px; cursor: pointer; }
</style>
```

## 2. Prompt Tuner

Interactive prompt engineering tool with preview and export.

```html
<div class="prompt-tuner">
  <h2>提示词调优器</h2>

  <div class="tuner-layout">
    <div class="editor-panel">
      <div class="param-group">
        <label>系统提示词</label>
        <textarea id="systemPrompt" rows="4">你是一个专业的技术文档写作者。</textarea>
      </div>
      <div class="param-group">
        <label>温度: <span id="tempValue">0.7</span></label>
        <input type="range" min="0" max="1" step="0.1" value="0.7" id="temperature"
               oninput="document.getElementById('tempValue').textContent = this.value">
      </div>
      <div class="param-group">
        <label>最大 Token: <span id="maxTokenValue">2000</span></label>
        <input type="range" min="100" max="4000" step="100" value="2000" id="maxTokens"
               oninput="document.getElementById('maxTokenValue').textContent = this.value">
      </div>
      <div class="param-group">
        <label>输出格式</label>
        <select id="outputFormat">
          <option value="markdown">Markdown</option>
          <option value="html">HTML</option>
          <option value="json">JSON</option>
        </select>
      </div>
    </div>

    <div class="preview-panel">
      <h3>配置预览</h3>
      <pre id="configPreview"></pre>
    </div>
  </div>

  <div class="tuner-actions">
    <button onclick="exportPrompt()">导出配置</button>
    <button onclick="copyPrompt()">复制到剪贴板</button>
  </div>
</div>

<script>
function updatePreview() {
  const config = {
    system: document.getElementById('systemPrompt').value,
    temperature: parseFloat(document.getElementById('temperature').value),
    max_tokens: parseInt(document.getElementById('maxTokens').value),
    output_format: document.getElementById('outputFormat').value
  };
  document.getElementById('configPreview').textContent = JSON.stringify(config, null, 2);
}

function exportPrompt() {
  const config = {
    system: document.getElementById('systemPrompt').value,
    temperature: parseFloat(document.getElementById('temperature').value),
    max_tokens: parseInt(document.getElementById('maxTokens').value),
    output_format: document.getElementById('outputFormat').value
  };
  const blob = new Blob([JSON.stringify(config, null, 2)], { type: 'application/json' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'prompt-config.json';
  a.click();
}

document.querySelectorAll('input, textarea, select').forEach(el => el.addEventListener('input', updatePreview));
updatePreview();
</script>

<style>
.tuner-layout { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
.param-group { margin-bottom: 16px; }
.param-group label { display: block; margin-bottom: 6px; color: var(--text-secondary); }
.param-group textarea, .param-group select { width: 100%; background: var(--bg-secondary); border: 1px solid var(--border); color: var(--text-primary); padding: 10px; border-radius: 6px; }
.param-group input[type="range"] { width: 100%; }
.preview-panel { background: var(--bg-card); padding: 16px; border-radius: 8px; }
.preview-panel pre { background: var(--bg-secondary); padding: 12px; border-radius: 6px; overflow: auto; font-family: monospace; font-size: 0.9em; }
.tuner-actions { margin-top: 20px; display: flex; gap: 12px; }
.tuner-actions button { padding: 10px 20px; background: var(--accent); color: white; border: none; border-radius: 6px; cursor: pointer; }
</style>
```

## 3. Markdown/Content Editor

Split-pane editor with live preview and export.

```html
<div class="content-editor">
  <div class="editor-toolbar">
    <button onclick="insertMarkdown('**', '**')" title="粗体">B</button>
    <button onclick="insertMarkdown('*', '*')" title="斜体">I</button>
    <button onclick="insertMarkdown('# ', '')" title="标题">H</button>
    <button onclick="insertMarkdown('`', '`')" title="代码">&lt;/&gt;</button>
    <button onclick="insertMarkdown('- ', '')" title="列表">☰</button>
  </div>

  <div class="editor-panes">
    <div class="editor-input">
      <textarea id="markdownInput" oninput="updatePreview()">
# 标题

这是内容示例。
      </textarea>
    </div>
    <div class="editor-preview" id="preview"></div>
  </div>

  <div class="editor-actions">
    <button onclick="exportMarkdown()">导出 Markdown</button>
    <button onclick="exportHTML()">导出 HTML</button>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/marked/marked.min.js"></script>
<script>
function updatePreview() {
  const input = document.getElementById('markdownInput').value;
  document.getElementById('preview').innerHTML = marked.parse(input);
}

function insertMarkdown(before, after) {
  const textarea = document.getElementById('markdownInput');
  const start = textarea.selectionStart;
  const end = textarea.selectionEnd;
  const text = textarea.value;
  const selected = text.substring(start, end);
  textarea.value = text.substring(0, start) + before + selected + after + text.substring(end);
  textarea.focus();
}

function exportMarkdown() {
  const content = document.getElementById('markdownInput').value;
  const blob = new Blob([content], { type: 'text/markdown' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'content.md';
  a.click();
}

function exportHTML() {
  const content = document.getElementById('preview').innerHTML;
  const blob = new Blob([content], { type: 'text/html' });
  const url = URL.createObjectURL(blob);
  const a = document.createElement('a');
  a.href = url;
  a.download = 'content.html';
  a.click();
}

updatePreview();
</script>

<style>
.editor-toolbar { display: flex; gap: 4px; padding: 8px; background: var(--bg-card); border-radius: 8px 8px 0 0; }
.editor-toolbar button { padding: 6px 12px; background: var(--bg-secondary); border: none; color: var(--text-primary); cursor: pointer; border-radius: 4px; }
.editor-toolbar button:hover { background: var(--accent); }
.editor-panes { display: grid; grid-template-columns: 1fr 1fr; gap: 0; border: 1px solid var(--border); }
.editor-input textarea { width: 100%; height: 400px; background: var(--bg-secondary); color: var(--text-primary); border: none; padding: 16px; font-family: monospace; resize: none; }
.editor-preview { padding: 16px; overflow: auto; max-height: 400px; }
.editor-actions { margin-top: 12px; display: flex; gap: 12px; }
.editor-actions button { padding: 10px 20px; background: var(--accent); color: white; border: none; border-radius: 6px; cursor: pointer; }
</style>
```
