---
layout: page
title: Skills Ledger
permalink: /skills/
---

[Dashboard](/dashboard/) | [Evidence](/evidence/) | [Home](/)

## 検索

<input id="skillFilter" type="text" placeholder="スキル名 / カテゴリ / next_action / evidence で絞り込み" style="width:100%;max-width:800px;padding:8px;">

{% assign sorted_skills = site.data.skills | sort: "name" %}
{% assign categories = "Frontend,Backend,DB,Infra,Quality,Other" | split: "," %}

{% for category in categories %}
## {{ category }}

<table>
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
              <a href="{{ link }}">{{ link }}</a>{% unless forloop.last %}, {% endunless %}
            {% endfor %}
          {% else %}
            -
          {% endif %}
        </td>
        <td>{{ skill.next_action }}</td>
        <td>{{ skill.priority_score }}</td>
      </tr>
      {% endif %}
    {% endfor %}
  </tbody>
</table>
{% endfor %}

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
