---
layout: post
title:  "My GitHub Repositories"
date:   2023-04-28 15:37:41 -0700
categories: repo
feed-type: repo
permalink: blog-repository/_posts/2023-04-28-github-repository
image: assets/images/3d-image1.jpg
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
