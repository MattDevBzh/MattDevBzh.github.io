---
layout: home
title: "Bienvenue sur mon blog tech"
---

Bienvenue sur mon blog !  
Je partage ici mes découvertes, tutoriels, et réflexions sur le développement .NET, Azure, DevOps, IA et plus encore.

👉 [Voir les derniers articles](./)
{% for post in site.posts %}
### [{{ post.title }}]({{ post.url }})
*{{ post.date | date: "%d %B %Y" }}*

{{ post.excerpt }}

---
{% endfor %}
Tu peux aussi consulter les catégories :
- .NET
- Azure
- DevOps
- IA

N'hésite pas à me contacter ou à commenter mes articles sur GitHub ! 🚀
