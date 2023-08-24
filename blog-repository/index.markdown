---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: "Repositories"
feed-type: repo
permalink: /blog-repository/index
categories: repo
---
<h1>My GitHub Repositories</h1>

<div id="repos">
  <ul id="repo-list"></ul>
</div>

<script>
fetch('https://api.github.com/users/Babigdk/repos')
  .then(response => response.json())
  .then(repos => {
    const repoList = document.getElementById('repo-list');
    repos.forEach(repo => {
      const listItem = document.createElement('li');
      const link = document.createElement('a');
      link.href = repo.html_url;
      link.textContent = repo.name;
      listItem.appendChild(link);
      repoList.appendChild(listItem);
    });
  });
</script>
