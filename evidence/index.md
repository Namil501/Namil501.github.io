---
layout: page
title: Evidence Ledger
permalink: /evidence/
---

<div class="modern-page evidence-page">
  <section class="modern-hero">
    <p class="hero-eyebrow">Evidence Ledger</p>
    <h1 class="hero-title">実績一覧</h1>
    <p class="hero-subtitle">案件ごとの期間・担当・成果・再現ポイントを記録し、スキルの根拠を明確化します。</p>
    <div class="nav-pills">
      <a href="/dashboard/">Dashboard</a>
      <a href="/skills/">Skills</a>
      <a href="/">Home</a>
    </div>
  </section>

  <section class="evidence-grid">
    {% for ev in site.data.evidence %}
    <article class="card evidence-card">
      <p class="hero-eyebrow">{{ ev.id }}</p>
      <h3>{{ ev.title }}</h3>
      <p class="evidence-meta">{{ ev.period }} / {{ ev.role }}</p>
      <div>
        {% for tech in ev.technologies %}
          <span class="tag">{{ tech }}</span>
        {% endfor %}
      </div>
      <p>{{ ev.result_summary }}</p>
      <a class="cta-link" href="{{ ev.link }}">詳細を見る →</a>
    </article>
    {% endfor %}
  </section>
</div>
