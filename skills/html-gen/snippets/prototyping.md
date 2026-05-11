# Prototyping Snippets

## 1. Draggable Kanban Board

Interactive kanban with drag-and-drop.

```html
<div class="kanban-board">
  <div class="kanban-column" data-status="todo">
    <h3>待办 <span class="count">3</span></h3>
    <div class="kanban-items">
      <div class="kanban-card" draggable="true" data-id="1">
        <div class="card-title">任务 1</div>
        <div class="card-meta">
          <span class="priority high">高</span>
          <span class="assignee">@user</span>
        </div>
      </div>
    </div>
  </div>
  <div class="kanban-column" data-status="progress">
    <h3>进行中 <span class="count">2</span></h3>
    <div class="kanban-items"></div>
  </div>
  <div class="kanban-column" data-status="done">
    <h3>完成 <span class="count">1</span></h3>
    <div class="kanban-items"></div>
  </div>
</div>

<script src="https://cdn.jsdelivr.net/npm/sortablejs@latest/Sortable.min.js"></script>
<script>
document.querySelectorAll('.kanban-items').forEach(el => {
  new Sortable(el, {
    group: 'kanban',
    animation: 150,
    ghostClass: 'card-ghost',
    onEnd: function(evt) {
      const cardId = evt.item.dataset.id;
      const newStatus = evt.to.closest('.kanban-column').dataset.status;
      console.log(`Card ${cardId} moved to ${newStatus}`);
    }
  });
});
</script>

<style>
.kanban-board { display: flex; gap: 20px; overflow-x: auto; padding: 20px; }
.kanban-column { min-width: 280px; background: var(--bg-secondary); border-radius: 12px; padding: 16px; }
.kanban-card { background: var(--bg-card); border-radius: 8px; padding: 12px; margin-bottom: 8px; cursor: grab; transition: transform 0.2s; }
.kanban-card:active { cursor: grabbing; }
.card-ghost { opacity: 0.4; }
.priority { padding: 2px 8px; border-radius: 4px; font-size: 0.8em; }
.priority.high { background: var(--error); }
.priority.medium { background: var(--warning); }
.priority.low { background: var(--success); }
</style>
```

## 2. Interactive Flow Builder

Click to add nodes, drag to connect.

```html
<div class="flow-builder">
  <div class="toolbar">
    <button onclick="addNode('start')">开始</button>
    <button onclick="addNode('process')">处理</button>
    <button onclick="addNode('decision')">判断</button>
    <button onclick="addNode('end')">结束</button>
  </div>
  <svg class="canvas" id="flowCanvas">
    <defs>
      <marker id="arrow" markerWidth="10" markerHeight="7" refX="10" refY="3.5" orient="auto">
        <polygon points="0 0, 10 3.5, 0 7" fill="#e94560"/>
      </marker>
    </defs>
  </svg>
</div>

<script>
let nodes = [];
let connections = [];
let selectedNode = null;

function addNode(type) {
  const id = nodes.length + 1;
  const node = { id, type, x: 100 + Math.random() * 400, y: 100 + Math.random() * 200 };
  nodes.push(node);
  render();
}

function render() {
  const svg = document.getElementById('flowCanvas');
  svg.innerHTML = svg.querySelector('defs').outerHTML;

  nodes.forEach(node => {
    const g = document.createElementNS('http://www.w3.org/2000/svg', 'g');
    g.setAttribute('transform', `translate(${node.x}, ${node.y})`);
    g.setAttribute('class', `node node-${node.type}`);
    g.setAttribute('data-id', node.id);

    const shapes = {
      start: `<rect width="100" height="50" rx="25" fill="#0f3460"/>`,
      process: `<rect width="100" height="50" rx="8" fill="#0f3460"/>`,
      decision: `<polygon points="50,0 100,50 50,100 0,50" fill="#0f3460"/>`,
      end: `<rect width="100" height="50" rx="25" fill="#e94560"/>`
    };

    g.innerHTML = shapes[node.type] + `<text x="50" y="30" text-anchor="middle" fill="white">${node.type}</text>`;
    svg.appendChild(g);
  });
}
</script>
```

## 3. Animation Debugger

Timeline-based animation control.

```html
<div class="animation-debugger">
  <div class="preview-area">
    <div class="animated-element" id="target"></div>
  </div>
  <div class="timeline-controls">
    <button onclick="play()">播放</button>
    <button onclick="pause()">暂停</button>
    <input type="range" min="0" max="100" value="0" id="timeline">
    <span id="timeDisplay">0.0s</span>
  </div>
  <div class="property-editor">
    <label>持续时间: <input type="number" value="1" id="duration">s</label>
    <label>缓动: <select id="easing">
      <option>ease</option>
      <option>linear</option>
      <option>ease-in-out</option>
    </select></label>
  </div>
</div>
```
