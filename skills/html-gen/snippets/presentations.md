# Presentations Snippets

## 1. Keyboard-Driven Slides

Full-screen presentation with keyboard navigation.

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { background: #1a1a2e; color: white; font-family: system-ui; overflow: hidden; }
    .slide { width: 100vw; height: 100vh; display: none; flex-direction: column; justify-content: center; align-items: center; padding: 60px; }
    .slide.active { display: flex; }
    .slide h1 { font-size: 3em; margin-bottom: 20px; }
    .slide h2 { font-size: 2em; color: #e94560; margin-bottom: 16px; }
    .slide p { font-size: 1.4em; max-width: 800px; text-align: center; line-height: 1.6; }
    .progress { position: fixed; bottom: 20px; right: 20px; font-size: 0.9em; color: #a0a0a0; }
    .controls { position: fixed; bottom: 20px; left: 20px; font-size: 0.8em; color: #a0a0a0; }
  </style>
</head>
<body>
  <div class="slide active" data-index="0">
    <h1>标题幻灯片</h1>
    <p>按 → 或空格键继续</p>
  </div>
  <div class="slide" data-index="1">
    <h2>第二页</h2>
    <p>内容内容内容</p>
  </div>
  <div class="progress"><span id="current">1</span> / <span id="total">2</span></div>
  <div class="controls">← → 翻页 | Esc 退出</div>

  <script>
    let current = 0;
    const slides = document.querySelectorAll('.slide');
    const total = slides.length;

    function showSlide(index) {
      slides.forEach(s => s.classList.remove('active'));
      slides[index].classList.add('active');
      document.getElementById('current').textContent = index + 1;
    }

    document.addEventListener('keydown', (e) => {
      if (e.key === 'ArrowRight' || e.key === ' ') {
        e.preventDefault();
        current = Math.min(current + 1, total - 1);
        showSlide(current);
      } else if (e.key === 'ArrowLeft') {
        e.preventDefault();
        current = Math.max(current - 1, 0);
        showSlide(current);
      }
    });
  </script>
</body>
</html>
```

## 2. Slide with Code Highlight

Presentation slide with syntax-highlighted code.

```html
<div class="slide">
  <h2>代码示例</h2>
  <div class="code-block">
    <div class="code-header">
      <span class="filename">example.js</span>
      <button class="copy-btn" onclick="copyCode()">复制</button>
    </div>
    <pre><code class="language-javascript">
function fibonacci(n) {
  if (n <= 1) return n;
  return fibonacci(n - 1) + fibonacci(n - 2);
}
    </code></pre>
  </div>
</div>

<style>
.code-block { background: #0d1117; border-radius: 8px; overflow: hidden; max-width: 700px; }
.code-header { display: flex; justify-content: space-between; align-items: center; padding: 8px 16px; background: #161b22; }
.filename { color: #a0a0a0; font-size: 0.9em; }
pre { padding: 20px; overflow-x: auto; }
code { font-family: 'Fira Code', monospace; font-size: 1.1em; }
</style>

<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/styles/github-dark.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/highlight.js/11.9.0/highlight.min.js"></script>
<script>hljs.highlightAll();</script>
```
