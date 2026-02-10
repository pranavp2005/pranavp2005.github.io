---
permalink: /
title: "About"
author_profile: true
---

Hi, I'm **Pranav**.

I'm pursuing a Master's of Science in Computer Science at Stony Brook University, where I focus on distributed systems and database systems. I am excited about solving difficult engineering challenges and building correct, secure and scalable systems.

I bring hands-on industry experience from working with the Platform Team at [Dremio](https://www.dremio.com/) and the Control Plane Team at [Datapelago](https://www.datapelago.ai/), where I tackled challenges in building performant and secure large-scale systems.

Currently, I'm working with Professor [Mohammad Javad Amiri's](https://www3.cs.stonybrook.edu/~amiri/index.html) research group, exploring isolation and consistency levels in database systems. My research aims to design databases with tunable consistency and isolation guarantees.

**I'm actively seeking Summer 2026 internship opportunities in distributed systems, databases, or infrastructure engineering.**

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

[Projects](/projects/) • [Resume/CV](/resume/) • [Blog](/year-archive/) • [Contact](/contact/)
