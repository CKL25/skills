# Reports Snippets

## 1. Weekly Report Template

Structured weekly report with sections.

```html
<div class="weekly-report">
  <header class="report-header">
    <h1>周报</h1>
    <div class="report-meta">
      <span class="date">2024年5月6日 - 5月10日</span>
      <span class="author">@developer</span>
    </div>
  </header>

  <section class="report-section">
    <h2>本周完成</h2>
    <div class="achievements">
      <div class="achievement-item">
        <span class="status done">✓</span>
        <div class="achievement-content">
          <h3>用户认证模块</h3>
          <p>完成 JWT 认证实现，包括登录、注册、token 刷新</p>
          <div class="metrics">
            <span class="metric">PR #123 已合并</span>
            <span class="metric">测试覆盖 92%</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="report-section">
    <h2>进行中</h2>
    <div class="progress-items">
      <div class="progress-item">
        <div class="progress-header">
          <h3>API 网关优化</h3>
          <span class="progress-pct">70%</span>
        </div>
        <div class="progress-bar">
          <div class="progress-fill" style="width: 70%;"></div>
        </div>
      </div>
    </div>
  </section>

  <section class="report-section">
    <h2>下周计划</h2>
    <ul class="plan-list">
      <li>完成 API 网关性能测试</li>
      <li>开始用户权限模块开发</li>
    </ul>
  </section>

  <section class="report-section">
    <h2>风险与阻塞</h2>
    <div class="risk-item">
      <span class="risk-level high">高</span>
      <p>第三方支付接口文档不完整，需要沟通确认</p>
    </div>
  </section>
</div>

<style>
.weekly-report { max-width: 800px; margin: 0 auto; }
.report-header { background: var(--bg-card); padding: 24px; border-radius: 12px; margin-bottom: 24px; }
.report-meta { display: flex; gap: 16px; margin-top: 8px; color: var(--text-secondary); }
.report-section { margin-bottom: 24px; }
.report-section h2 { color: var(--accent); border-bottom: 2px solid var(--border); padding-bottom: 8px; margin-bottom: 16px; }
.achievement-item { display: flex; gap: 12px; padding: 12px; background: var(--bg-card); border-radius: 8px; margin-bottom: 8px; }
.status.done { color: var(--success); font-size: 1.2em; }
.metrics { display: flex; gap: 12px; margin-top: 8px; }
.metric { background: var(--bg-secondary); padding: 4px 10px; border-radius: 4px; font-size: 0.85em; }
.progress-bar { height: 8px; background: var(--bg-secondary); border-radius: 4px; overflow: hidden; }
.progress-fill { height: 100%; background: var(--accent); transition: width 0.3s; }
.risk-item { display: flex; gap: 12px; align-items: center; padding: 12px; background: var(--bg-card); border-radius: 8px; }
.risk-level { padding: 4px 10px; border-radius: 4px; font-size: 0.85em; font-weight: bold; }
.risk-level.high { background: var(--error); }
.risk-level.medium { background: var(--warning); }
.risk-level.low { background: var(--success); }
</style>
```

## 2. Incident Timeline

Visual timeline for incident reports.

```html
<div class="incident-timeline">
  <h2>事故时间线 - 2024-05-10 服务中断</h2>

  <div class="timeline">
    <div class="timeline-item critical">
      <div class="timeline-time">14:32</div>
      <div class="timeline-content">
        <h3>告警触发</h3>
        <p>API 响应时间超过阈值，PagerDuty 触发告警</p>
        <span class="impact">影响: 所有用户</span>
      </div>
    </div>

    <div class="timeline-item warning">
      <div class="timeline-time">14:35</div>
      <div class="timeline-content">
        <h3>开始排查</h3>
        <p>oncall 工程师开始检查服务状态</p>
      </div>
    </div>

    <div class="timeline-item info">
      <div class="timeline-time">14:45</div>
      <div class="timeline-content">
        <h3>根因定位</h3>
        <p>数据库连接池耗尽，原因是慢查询</p>
      </div>
    </div>

    <div class="timeline-item success">
      <div class="timeline-time">15:10</div>
      <div class="timeline-content">
        <h3>问题修复</h3>
        <p>重启服务并增加连接池大小</p>
      </div>
    </div>
  </div>
</div>

<style>
.timeline { position: relative; padding-left: 40px; }
.timeline::before { content: ''; position: absolute; left: 20px; top: 0; bottom: 0; width: 2px; background: var(--border); }
.timeline-item { position: relative; margin-bottom: 24px; }
.timeline-item::before { content: ''; position: absolute; left: -28px; top: 8px; width: 12px; height: 12px; border-radius: 50%; border: 2px solid var(--border); background: var(--bg-primary); }
.timeline-item.critical::before { border-color: var(--error); background: var(--error); }
.timeline-item.warning::before { border-color: var(--warning); background: var(--warning); }
.timeline-item.info::before { border-color: #2196f3; background: #2196f3; }
.timeline-item.success::before { border-color: var(--success); background: var(--success); }
.timeline-time { font-family: monospace; color: var(--text-secondary); margin-bottom: 4px; }
.timeline-content { background: var(--bg-card); padding: 16px; border-radius: 8px; }
.impact { display: inline-block; margin-top: 8px; padding: 4px 10px; background: rgba(244, 67, 54, 0.2); border-radius: 4px; font-size: 0.85em; }
</style>
```

## 3. Status Dashboard

Multi-service status overview.

```html
<div class="status-dashboard">
  <h2>系统状态</h2>
  <div class="overall-status operational">所有系统正常运行</div>

  <div class="services-grid">
    <div class="service-card">
      <div class="service-header">
        <h3>API 服务</h3>
        <span class="status-dot operational"></span>
      </div>
      <div class="service-metrics">
        <div class="metric">
          <span class="metric-label">响应时间</span>
          <span class="metric-value">45ms</span>
        </div>
        <div class="metric">
          <span class="metric-label">可用性</span>
          <span class="metric-value">99.9%</span>
        </div>
      </div>
    </div>
  </div>
</div>

<style>
.overall-status { padding: 16px; border-radius: 8px; text-align: center; font-size: 1.2em; margin-bottom: 24px; }
.overall-status.operational { background: rgba(76, 175, 80, 0.2); color: var(--success); }
.services-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 16px; }
.service-card { background: var(--bg-card); padding: 16px; border-radius: 8px; }
.service-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 12px; }
.status-dot { width: 12px; height: 12px; border-radius: 50%; }
.status-dot.operational { background: var(--success); }
.status-dot.degraded { background: var(--warning); }
.status-dot.down { background: var(--error); }
</style>
```
