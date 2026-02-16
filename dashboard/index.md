---
layout: page
title: Skill Dashboard
permalink: /dashboard/
---

<div class="modern-page dashboard-page">
  <section class="modern-hero">
    <p class="hero-eyebrow">Skill Command Center</p>
    <h1 class="hero-title">個人スキルダッシュボード</h1>
    <p class="hero-subtitle">強み・課題・次アクションを一箇所で管理し、運用/品質重視で成長の優先順位を可視化します。</p>
    <div class="nav-pills">
      <a href="/skills/">Skills</a>
      <a href="/evidence/">Evidence</a>
      <a href="/">Home</a>
    </div>
  </section>

  {% assign total_skills = site.data.skills | size %}
  {% assign total_evidence = site.data.evidence | size %}
  {% assign confidence_a = site.data.skills | where: "confidence", "A" | size %}

  <section class="grid-3">
    <article class="card mini-stat">
      <span class="label">Role</span>
      <span class="value role-value">{{ site.data.goals.role }}</span>
    </article>
    <article class="card mini-stat">
      <span class="label">Skills</span>
      <span class="value">{{ total_skills }}</span>
    </article>
    <article class="card mini-stat">
      <span class="label">Evidence / Confidence A</span>
      <span class="value">{{ total_evidence }} / {{ confidence_a }}</span>
    </article>
  </section>

  <h2 class="section-title">注力テーマ</h2>
  <section class="grid-3">
    <article class="card">
      <h3>3ヶ月</h3>
      <ul class="list-tight">
        {% for item in site.data.goals.focus_3m %}
        <li>{{ item }}</li>
        {% endfor %}
      </ul>
    </article>
    <article class="card">
      <h3>6ヶ月</h3>
      <ul class="list-tight">
        {% for item in site.data.goals.focus_6m %}
        <li>{{ item }}</li>
        {% endfor %}
      </ul>
    </article>
    <article class="card">
      <h3>12ヶ月</h3>
      <ul class="list-tight">
        {% for item in site.data.goals.focus_12m %}
        <li>{{ item }}</li>
        {% endfor %}
      </ul>
    </article>
  </section>

  {% assign strengths = site.data.skills | sort: "strength_score" | reverse %}
  {% assign weak_points = site.data.skills | sort: "priority_score" | reverse %}

  <h2 class="section-title">強み Top5</h2>
  <article class="card">
    <div class="table-scroll">
      <table class="modern-table">
        <thead>
          <tr>
            <th>Skill</th>
            <th>Category</th>
            <th>Level</th>
            <th>Confidence</th>
            <th>Evidence</th>
            <th>Strength Score</th>
          </tr>
        </thead>
        <tbody>
          {% for skill in strengths limit:5 %}
          <tr>
            <td>{{ skill.name }}</td>
            <td>{{ skill.category }}</td>
            <td>{{ skill.level }}</td>
            <td>{{ skill.confidence }}</td>
            <td>{{ skill.evidence | size }}</td>
            <td><span class="score-pill">{{ skill.strength_score }}</span></td>
          </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
  </article>

  <h2 class="section-title">弱み Top5（優先度）</h2>
  <article class="card">
    <div class="table-scroll">
      <table class="modern-table">
        <thead>
          <tr>
            <th>Skill</th>
            <th>Gap</th>
            <th>Stale</th>
            <th>No Evidence</th>
            <th>Low Confidence</th>
            <th>Priority</th>
          </tr>
        </thead>
        <tbody>
          {% for skill in weak_points limit:5 %}
          {% assign gap = skill.target.m3 | minus: skill.level %}
          {% if gap < 0 %}{% assign gap = 0 %}{% endif %}
          <tr>
            <td>{{ skill.name }}</td>
            <td>{{ gap }}</td>
            <td>{{ skill.stale_score }}</td>
            <td>{{ skill.no_evidence }}</td>
            <td>{{ skill.low_confidence }}</td>
            <td><span class="score-pill">{{ skill.priority_score }}</span></td>
          </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
  </article>

  <h2 class="section-title">直近90日の次アクション Top10</h2>
  <article class="card">
    <div class="table-scroll">
      <table class="modern-table">
        <thead>
          <tr>
            <th>Rank</th>
            <th>Skill</th>
            <th>Priority</th>
            <th>Next Action</th>
            <th>Last Used</th>
          </tr>
        </thead>
        <tbody>
          {% for skill in weak_points limit:10 %}
          <tr>
            <td>{{ forloop.index }}</td>
            <td>{{ skill.name }}</td>
            <td><span class="score-pill">{{ skill.priority_score }}</span></td>
            <td>{{ skill.next_action }}</td>
            <td>{{ skill.last_used }}</td>
          </tr>
          {% endfor %}
        </tbody>
      </table>
    </div>
    <p class="formula">
      gap = max(target.m3 - level, 0) / priority_score = gap*3 + stale_score*2 + no_evidence*2 + low_confidence*1 / 基準日: 2026-02
    </p>
  </article>
</div>
