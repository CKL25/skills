# Charts & Illustrations Snippets

## 1. SVG Flowchart

Auto-layout flowchart with connectors.

```html
<div class="flowchart">
  <svg viewBox="0 0 800 500" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <marker id="arrowhead" markerWidth="10" markerHeight="7" refX="10" refY="3.5" orient="auto">
        <polygon points="0 0, 10 3.5, 0 7" fill="#e94560"/>
      </marker>
      <filter id="shadow">
        <feDropShadow dx="2" dy="2" stdDeviation="3" flood-opacity="0.3"/>
      </filter>
    </defs>

    <!-- Start -->
    <rect x="350" y="20" width="100" height="50" rx="25" fill="#4caf50" filter="url(#shadow)"/>
    <text x="400" y="50" text-anchor="middle" fill="white">开始</text>

    <!-- Process -->
    <rect x="325" y="120" width="150" height="60" rx="8" fill="#0f3460" filter="url(#shadow)"/>
    <text x="400" y="155" text-anchor="middle" fill="white">处理数据</text>

    <!-- Decision -->
    <polygon points="400,240 470,290 400,340 330,290" fill="#e94560" filter="url(#shadow)"/>
    <text x="400" y="295" text-anchor="middle" fill="white">有效?</text>

    <!-- Connections -->
    <line x1="400" y1="70" x2="400" y2="120" stroke="#e94560" stroke-width="2" marker-end="url(#arrowhead)"/>
    <line x1="400" y1="180" x2="400" y2="240" stroke="#e94560" stroke-width="2" marker-end="url(#arrowhead)"/>

    <!-- Yes/No branches -->
    <line x1="470" y1="290" x2="600" y2="290" stroke="#4caf50" stroke-width="2" marker-end="url(#arrowhead)"/>
    <text x="530" y="280" fill="#4caf50">是</text>

    <line x1="400" y1="340" x2="400" y2="420" stroke="#f44336" stroke-width="2" marker-end="url(#arrowhead)"/>
    <text x="415" y="380" fill="#f44336">否</text>
  </svg>
</div>
```

## 2. Interactive Pie Chart

Hover to see details, click to filter.

```html
<div class="chart-container">
  <canvas id="pieChart" width="400" height="400"></canvas>
  <div class="chart-legend" id="legend"></div>
</div>

<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
const ctx = document.getElementById('pieChart').getContext('2d');
const chart = new Chart(ctx, {
  type: 'doughnut',
  data: {
    labels: ['前端', '后端', '数据库', 'DevOps', '测试'],
    datasets: [{
      data: [30, 25, 20, 15, 10],
      backgroundColor: ['#e94560', '#0f3460', '#4caf50', '#ff9800', '#9c27b0']
    }]
  },
  options: {
    responsive: true,
    plugins: {
      legend: { position: 'right' }
    }
  }
});
</script>
```

## 3. Network/Architecture Diagram

SVG-based system architecture.

```html
<div class="architecture-diagram">
  <svg viewBox="0 0 900 600" xmlns="http://www.w3.org/2000/svg">
    <!-- Client Layer -->
    <rect x="50" y="50" width="800" height="100" rx="8" fill="rgba(15, 52, 96, 0.3)" stroke="#0f3460"/>
    <text x="450" y="80" text-anchor="middle" fill="#a0a0a0">客户端层</text>
    <rect x="80" y="90" width="80" height="40" rx="6" fill="#0f3460"/>
    <text x="120" y="115" text-anchor="middle" fill="white">Web</text>
    <rect x="200" y="90" width="80" height="40" rx="6" fill="#0f3460"/>
    <text x="240" y="115" text-anchor="middle" fill="white">Mobile</text>

    <!-- Service Layer -->
    <rect x="50" y="200" width="800" height="150" rx="8" fill="rgba(233, 69, 96, 0.1)" stroke="#e94560"/>
    <text x="450" y="230" text-anchor="middle" fill="#a0a0a0">服务层</text>
    <rect x="100" y="250" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="160" y="285" text-anchor="middle" fill="white">API Gateway</text>
    <rect x="300" y="250" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="360" y="285" text-anchor="middle" fill="white">Auth Service</text>
    <rect x="500" y="250" width="120" height="60" rx="8" fill="#0f3460"/>
    <text x="560" y="285" text-anchor="middle" fill="white">User Service</text>

    <!-- Connections -->
    <line x1="120" y1="130" x2="160" y2="250" stroke="#e94560" stroke-width="1.5" stroke-dasharray="5,5"/>
    <line x1="240" y1="130" x2="160" y2="250" stroke="#e94560" stroke-width="1.5" stroke-dasharray="5,5"/>
  </svg>
</div>
```
