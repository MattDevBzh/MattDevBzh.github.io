---
layout: default
title: "Bienvenue sur mon blog tech"
---

## Bienvenue sur mon blog tech ! 👋

Bienvenue sur mon blog !  
Je partage ici mes découvertes, tutoriels, et réflexions sur le développement .NET, Azure, DevOps, IA et plus encore.

## 📚 Tous mes articles

{% if site.posts.size > 0 %}
<div class="post-list">
{% for post in site.posts %}
  <article class="post-item">
    <h3><a href="{{ post.url | relative_url }}">{{ post.title | escape }}</a></h3>
    <p class="post-meta">{{ post.date | date: "%d %B %Y" }}</p>
    <div class="post-excerpt">{{ post.excerpt }}</div>
  </article>
{% endfor %}
</div>
{% else %}
<p>Aucun article pour le moment.</p>
{% endif %}

---

## 🏷️ Catégories

Tu peux aussi consulter les catégories :
- .NET
- Azure  
- DevOps
- IA

N'hésite pas à me contacter ou à commenter mes articles sur GitHub ! 🚀
