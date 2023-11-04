---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: "GitHub Repositories"
feed-type: repo
<!-- permalink: blog-repository/index.markdown -->
categories: repo
---

<h2></h2>

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Description</th>
      <th>Language</th>
    </tr>
  </thead>
  <tbody>
    {% assign repositories = site.github.public_repositories %}
    {% for repository in repositories %}
      <tr>
        <td><a href="{{ repository.html_url }}">{{ repository.name }}</a></td>
        <td>{{ repository.description | default: "N/A" }}</td>
        <td>{{ repository.language | default: "N/A" }}</td>
      </tr>
    {% endfor %}
  </tbody>
</table>
