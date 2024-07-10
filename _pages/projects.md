---
layout: page
title: notes
permalink: /notes/
description: ML, math, & research notes (constantly in progress/updated)
nav: true
nav_order: 1
horizontal: false
---

<!-- pages/projects.md -->

<div class="projects">

{%- assign sorted_projects = site.projects | sort: "importance" -%}

<!-- Generate smaller text-only clickable cards for each project stacked vertically -->

<div class="container">
  {%- for project in sorted_projects -%}
    <a href="{{ project.url }}" class="card mb-3 text-decoration-none text-reset">
      <div class="card-body">
        <h5 class="card-title">{{ project.title }}</h5>
        <p class="card-text">{{ project.description }}</p>
      </div>
    </a>
  {%- endfor %}
</div>

</div>