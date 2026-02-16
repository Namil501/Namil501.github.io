---
layout: page
title: Skill Dashboard
permalink: /dashboard/
---

[Skills](/skills/) | [Evidence](/evidence/) | [Home](/)

## 目標ロール

{{ site.data.goals.role }}

## 注力テーマ

### 3ヶ月
{% for item in site.data.goals.focus_3m %}
- {{ item }}
{% endfor %}

### 6ヶ月
{% for item in site.data.goals.focus_6m %}
- {{ item }}
{% endfor %}

### 12ヶ月
{% for item in site.data.goals.focus_12m %}
- {{ item }}
{% endfor %}

---

## 強み Top5

{% assign strengths = site.data.skills | sort: "strength_score" | reverse %}

| Skill | Category | Level | Confidence | Evidence | Strength Score |
|---|---|---:|:---:|---:|---:|
{% for skill in strengths limit:5 %}
| {{ skill.name }} | {{ skill.category }} | {{ skill.level }} | {{ skill.confidence }} | {{ skill.evidence | size }} | {{ skill.strength_score }} |
{% endfor %}

## 弱み Top5（優先度）

{% assign weak_points = site.data.skills | sort: "priority_score" | reverse %}

| Skill | Gap(m3-level) | Stale | No Evidence | Low Confidence | Priority |
|---|---:|---:|---:|---:|---:|
{% for skill in weak_points limit:5 %}
{% assign gap = skill.target.m3 | minus: skill.level %}
{% if gap < 0 %}{% assign gap = 0 %}{% endif %}
| {{ skill.name }} | {{ gap }} | {{ skill.stale_score }} | {{ skill.no_evidence }} | {{ skill.low_confidence }} | {{ skill.priority_score }} |
{% endfor %}

## 直近90日の次アクション Top10

| Rank | Skill | Priority | Next Action | Last Used |
|---:|---|---:|---|---|
{% for skill in weak_points limit:10 %}
| {{ forloop.index }} | {{ skill.name }} | {{ skill.priority_score }} | {{ skill.next_action }} | {{ skill.last_used }} |
{% endfor %}

## スコア式（基準日: 2026-02）

- `gap = max(target.m3 - level, 0)`
- `priority_score = gap*3 + stale_score*2 + no_evidence*2 + low_confidence*1`
- `stale_score` は最終利用年月から算出（0〜5段階）
