---
layout: page
title: Evidence Ledger
permalink: /evidence/
---

[Dashboard](/dashboard/) | [Skills](/skills/) | [Home](/)

## Evidence 一覧

{% assign evidences = site.data.evidence %}

| ID | Title | Period | Role | Technologies | Link |
|---|---|---|---|---|---|
{% for ev in evidences %}
| {{ ev.id }} | {{ ev.title }} | {{ ev.period }} | {{ ev.role }} | {{ ev.technologies | join: ", " }} | [Open]({{ ev.link }}) |
{% endfor %}
