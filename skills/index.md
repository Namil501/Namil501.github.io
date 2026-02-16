---
layout: page
title: Skills Ledger
permalink: /skills/
---

<div class="modern-page skills-page">
  <section class="modern-hero">
    <p class="hero-eyebrow">Skill Ledger</p>
    <h1 class="hero-title">スキル台帳</h1>
    <p class="hero-subtitle">カテゴリ別にスキル・目標・根拠・次アクションを管理します。検索欄で瞬時に絞り込みできます。</p>
    <div class="nav-pills">
      <a href="/dashboard/">Dashboard</a>
      <a href="/evidence/">Evidence</a>
      <a href="/">Home</a>
    </div>
  </section>

  <section class="card">
    <input id="skillFilter" class="search-input" type="text" placeholder="スキル名 / カテゴリ / next_action / evidence で絞り込み">
  </section>

  {% assign sorted_skills = site.data.skills | sort: "name" %}
  {% assign categories = "Frontend,Backend,DB,Infra,Quality,Other" | split: "," %}

  {% for category in categories %}
  {% assign category_items = sorted_skills | where: "category", category %}
  <h2 class="section-title">{{ category }} <span class="tag">{{ category_items | size }} skills</span></h2>

  <article class="card">
    <table class="modern-table">
      <thead>
        <tr>
          <th>Skill</th>
          <th>Level</th>
          <th>Confidence</th>
          <th>Last Used</th>
          <th>Target (m3/m6/m12)</th>
          <th>Evidence</th>
          <th>Next Action</th>
          <th>Priority</th>
        </tr>
      </thead>
      <tbody>
        {% for skill in sorted_skills %}
        {% if skill.category == category %}
        <tr class="skill-row"
            data-skill="{{ skill.name | downcase }}"
            data-category="{{ skill.category | downcase }}"
            data-next="{{ skill.next_action | downcase }}"
            data-evidence="{{ skill.evidence | join: ' ' | downcase }}">
          <td>{{ skill.name }}</td>
          <td>{{ skill.level }}</td>
          <td>{{ skill.confidence }}</td>
          <td>{{ skill.last_used }}</td>
          <td>{{ skill.target.m3 }}/{{ skill.target.m6 }}/{{ skill.target.m12 }}</td>
          <td>
            {% if skill.evidence and skill.evidence.size > 0 %}
              {% for link in skill.evidence %}
                <a class="cta-link" href="{{ link }}">{{ link }}</a>{% unless forloop.last %}<br>{% endunless %}
              {% endfor %}
            {% else %}
              <span class="tag">No evidence</span>
            {% endif %}
          </td>
          <td>{{ skill.next_action }}</td>
          <td><span class="score-pill">{{ skill.priority_score }}</span></td>
        </tr>
        {% endif %}
        {% endfor %}
      </tbody>
    </table>
  </article>
  {% endfor %}
</div>

<script>
(function () {
  var input = document.getElementById('skillFilter');
  if (!input) return;

  function applyFilter() {
    var q = (input.value || '').toLowerCase().trim();
    var rows = document.querySelectorAll('tr.skill-row');
    for (var i = 0; i < rows.length; i++) {
      var row = rows[i];
      var haystack = [
        row.getAttribute('data-skill') || '',
        row.getAttribute('data-category') || '',
        row.getAttribute('data-next') || '',
        row.getAttribute('data-evidence') || ''
      ].join(' ');
      row.style.display = !q || haystack.indexOf(q) >= 0 ? '' : 'none';
    }
  }

  input.addEventListener('input', applyFilter);
})();
</script>
