# Design Snippets

## 1. Color Palette Showcase

Interactive color palette with copy-to-clipboard.

```html
<div class="palette-showcase">
  <h3>设计系统色板</h3>
  <div class="palette-group">
    <h4>主色调</h4>
    <div class="color-row">
      <div class="color-swatch" style="background: #e94560;" data-hex="#e94560">
        <span class="color-name">Primary</span>
        <span class="color-hex">#e94560</span>
      </div>
      <div class="color-swatch" style="background: #0f3460;" data-hex="#0f3460">
        <span class="color-name">Secondary</span>
        <span class="color-hex">#0f3460</span>
      </div>
    </div>
  </div>
</div>

<script>
document.querySelectorAll('.color-swatch').forEach(swatch => {
  swatch.addEventListener('click', () => {
    const hex = swatch.dataset.hex;
    navigator.clipboard.writeText(hex);
    swatch.classList.add('copied');
    setTimeout(() => swatch.classList.remove('copied'), 1000);
  });
});
</script>

<style>
.color-row { display: flex; gap: 12px; flex-wrap: wrap; }
.color-swatch { width: 120px; height: 100px; border-radius: 12px; display: flex; flex-direction: column; justify-content: flex-end; padding: 10px; cursor: pointer; transition: transform 0.2s; color: white; text-shadow: 0 1px 2px rgba(0,0,0,0.3); }
.color-swatch:hover { transform: scale(1.05); }
.color-swatch.copied::after { content: '已复制!'; position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); background: rgba(0,0,0,0.8); padding: 4px 8px; border-radius: 4px; }
.color-name { font-weight: bold; }
.color-hex { font-size: 0.85em; opacity: 0.9; }
</style>
```

## 2. Component Variant Grid

Show component states and variants.

```html
<div class="variant-grid">
  <h3>按钮组件变体</h3>
  <div class="variant-section">
    <h4>尺寸</h4>
    <div class="variant-row">
      <button class="btn btn-sm">Small</button>
      <button class="btn btn-md">Medium</button>
      <button class="btn btn-lg">Large</button>
    </div>
  </div>
  <div class="variant-section">
    <h4>状态</h4>
    <div class="variant-row">
      <button class="btn btn-primary">Primary</button>
      <button class="btn btn-secondary">Secondary</button>
      <button class="btn btn-outline">Outline</button>
      <button class="btn btn-disabled" disabled>Disabled</button>
    </div>
  </div>
</div>

<style>
.btn { border: none; border-radius: 6px; cursor: pointer; font-weight: 500; transition: all 0.2s; }
.btn-sm { padding: 6px 12px; font-size: 0.85em; }
.btn-md { padding: 8px 16px; }
.btn-lg { padding: 12px 24px; font-size: 1.1em; }
.btn-primary { background: var(--accent); color: white; }
.btn-secondary { background: var(--bg-card); color: var(--text-primary); }
.btn-outline { background: transparent; border: 2px solid var(--accent); color: var(--accent); }
.btn-disabled { opacity: 0.5; cursor: not-allowed; }
.variant-row { display: flex; gap: 12px; align-items: center; flex-wrap: wrap; }
</style>
```

## 3. Typography Scale

Font size and weight visualization.

```html
<div class="typography-scale">
  <div class="type-sample" style="font-size: 3em; font-weight: 700;">
    <span class="type-label">H1 - 3em Bold</span>
    <span class="type-text">标题文字示例</span>
  </div>
  <div class="type-sample" style="font-size: 2em; font-weight: 600;">
    <span class="type-label">H2 - 2em Semibold</span>
    <span class="type-text">副标题示例</span>
  </div>
  <div class="type-sample" style="font-size: 1em; font-weight: 400;">
    <span class="type-label">Body - 1em Regular</span>
    <span class="type-text">正文文字示例，用于主要内容展示</span>
  </div>
</div>
```
