---
permalink: /
title: "About"
author_profile: true
---

Hi, I'm **Pranav**.

I'm pursuing Master's of Science in Computer Science at Stony Brook University. My interests are distributed systems and database systems broadly and I am always excited to learn more about distributed systems and apply that learning to solving difficult engineering challenges and building correct, secure, and scalable systems.

I have 3+ years of industry experience as a Software Engineer, including work on the Platform Team at [Dremio](https://www.dremio.com/) and the Control Plane Team at [Datapelago](https://www.datapelago.ai/). Across both roles, I have built cloud-native control plane services for datalakehouse platforms; spanning authentication/RBAC, job orchestration, and Kubernetes-based cluster lifecycle management, with a focus on performance, observability, and security.

At Stony Brook University, I am working at Professor [Mohammad Javad Amiri's](https://www3.cs.stonybrook.edu/~amiri/index.html) research group, exploring isolation and consistency levels in database systems. My research aims to design databases with tunable consistency and isolation guarantees.

**I'm actively seeking Summer 2026 internship opportunities in distributed systems, databases, or infrastructure engineering.**

Outside of academics, I like slowing down with movies and getting outdoors to explore new cities and trails.

## News

{% assign news_items = site.data.news.items | default: empty %}

<div class="about-news" role="region" aria-label="Recent news and updates">
  <ul class="about-news__list">
    {% if news_items == empty %}
      <li class="about-news__item">
        <span class="about-news__date">--</span>
        <span>No updates yet.</span>
      </li>
    {% else %}
      {% for item in news_items %}
      <li class="about-news__item">
        <span class="about-news__date">{{ item.date }}</span>
        <span>{{ item.body | markdownify | remove: "<p>" | remove: "</p>" }}</span>
      </li>
      {% endfor %}
    {% endif %}
  </ul>
</div>

---

**Explore More**

[Resume/CV](/resume/) • [Projects](/projects/) • [Contact](/contact/)
