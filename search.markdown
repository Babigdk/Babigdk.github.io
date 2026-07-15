---
layout: page
title: Search
---

<div class="search-container">
  <input type="search" id="search-input" placeholder="Search posts..." aria-label="Search posts">
  <ul id="search-results"></ul>
  <p id="search-no-results" hidden>No results found.</p>
</div>

<script src="https://cdnjs.cloudflare.com/ajax/libs/lunr.js/2.3.9/lunr.min.js"></script>
<script>
  let lunrIndex;
  let pages;

  fetch('{{ "/search.json" | relative_url }}')
    .then(response => response.json())
    .then(data => {
      pages = data;
      lunrIndex = lunr(function () {
        this.ref('url');
        this.field('title', { boost: 10 });
        this.field('tags', { boost: 5 });
        this.field('content');
        pages.forEach(page => this.add(page));
      });
    });

  const input = document.getElementById('search-input');
  const results = document.getElementById('search-results');
  const noResults = document.getElementById('search-no-results');

  input.addEventListener('input', function () {
    const query = input.value.trim();
    results.innerHTML = '';

    if (!query || !lunrIndex) {
      noResults.hidden = true;
      return;
    }

    const matches = lunrIndex.search(query);
    noResults.hidden = matches.length > 0;

    matches.forEach(match => {
      const page = pages.find(p => p.url === match.ref);
      const li = document.createElement('li');
      li.innerHTML = '<a href="' + page.url + '">' + page.title + '</a>' +
        '<span class="search-meta">' + page.date + '</span>' +
        '<p>' + page.content + '</p>';
      results.appendChild(li);
    });
  });
</script>
