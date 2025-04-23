---
layout: attic-layout
title: Process Tracking
---

<!-- sort projects by descending "retirement_date" -->
{%- assign projects_by_date = site.data.project_array | sort: "retirement_date" | reverse %}
{%- assign list_date_fmt = "%b %Y" %}

<div class="section-content">
<p>
  <table>
    <tr><th>Retirement<br />Date</th><th>Attic Move<br />Completed</th><th>Project</th><th>Attic<br />Tracking</th></tr>
    {%- for project in projects_by_date %}
    <tr>
      <td>{{ project.retirement_date | date: list_date_fmt }}</td>
      <td>{{ project.attic_date | date: list_date_fmt }}</td>
      <td><a href="/projects/{{ project.project_id }}.html">Apache {{ project.project_name }}</a></td>
      <td>
      {%- if project.attic_issue -%}
        <a href="https://issues.apache.org/jira/browse/{{ project.attic_issue }}">{{ project.attic_issue }}</a>
      {%- else -%}
        -
      {%- endif -%}
      </td>
    </tr>
    {% endfor %}
  </table>
</p>
</div>


