---
layout: attic-layout
title: Process Tracking
---

{% capture project_list %}
{%- for proj_hash in site.data.projects -%}
  {%- unless forloop.first %},{% endunless -%}
  {{proj_hash[1].retirement_date | proj_hash[1].completion_date | append: ":" | append: proj_hash[0] }}
{%- endfor -%}
{% endcapture %}
{% assign project_array = project_list | split: "," | sort | reverse %}
{% assign list_date_fmt = "%b %Y" %}

<div class="section-content">
<p>
  <table>
    <tr><th>Retirement<br />Date</th><th>Attic Move<br />Completed</th><th>Project</th><th>Attic<br />Tracking</th></tr>
    {%- for project_ref in project_array %}
      {%- assign project_id   = project_ref | split: ":" | last -%}
      {%- assign project      = site.data.projects[project_id] -%}
      {%- assign default_name = project_id | capitalize -%}
      {%- assign project_name = project.project_name | default: default_name -%}
      {%- if project_id != "_template" %}
        <tr>
          <td>{{ project.retirement_date | date: list_date_fmt }}</td>
          <td>{{ project.attic_date | date: list_date_fmt }}</td>
          <td><a href="/projects/{{ project_id }}.html">Apache {{ project_name }}</a></td>
          <td>
          {%- if project.attic_issue -%}
            <a href="https://issues.apache.org/jira/browse/{{ project.attic_issue }}">{{ project.attic_issue }}</a>
          {%- else -%}
            -
          {%- endif -%}
          </td>
        </tr>
      {%- endif -%}
    {% endfor %}
  </table>
</p>
</div>


