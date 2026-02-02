---
layout: single
title: "Bookshelf"
permalink: /bookshelf/
author_profile: true
---

{% include base_path %}

A living list of books and papers I am reading or have finished.

## Books

{% assign books = site.data.books.books | default: empty %}

{% if books == empty or books.size == 0 %}
No books yet. (Edit `_data/books.yml` to add some.)
{% else %}

<div class="bookshelf__grid">
{% for item in books %}
  {% if item.image %}
    {% if item.image contains "://" %}
      {% assign cover = item.image %}
    {% else %}
      {% assign cover = item.image | prepend: "/" | prepend: base_path %}
    {% endif %}
  {% else %}
    {% assign cover = "/images/500x300.png" | prepend: base_path %}
  {% endif %}
  {% assign status = item.status | default: "Queued" | downcase %}

  <article class="bookshelf__card">
    <div class="bookshelf__cover">
      <img src="{{ cover }}" alt="{{ item.title }} cover" loading="lazy">
      <span class="bookshelf__status bookshelf__status--{{ status }}">{{ item.status | default: "Queued" }}</span>
    </div>
    <div class="bookshelf__meta">
      <h3 class="bookshelf__title">{{ item.title }}</h3>
      {% if item.author %}<p class="bookshelf__author">{{ item.author }}</p>{% endif %}
      {% if item.notes and item.notes != "" %}
        <div class="bookshelf__notes">{{ item.notes | markdownify }}</div>
      {% endif %}
    </div>
  </article>
{% endfor %}
</div>

{% endif %}

## Papers

{% assign papers = site.data.books.papers | default: empty %}

{% if papers == empty or papers.size == 0 %}
No papers yet. (Edit `_data/books.yml` to add some.)
{% else %}

<div class="bookshelf__grid">
{% for item in papers %}
  {% if item.image %}
    {% if item.image contains "://" %}
      {% assign cover = item.image %}
    {% else %}
      {% assign cover = item.image | prepend: "/" | prepend: base_path %}
    {% endif %}
  {% else %}
    {% assign cover = "/images/500x300.png" | prepend: base_path %}
  {% endif %}
  {% assign status = item.status | default: "Queued" | downcase %}

  <article class="bookshelf__card">
    <div class="bookshelf__cover">
      <img src="{{ cover }}" alt="{{ item.title }} cover" loading="lazy">
      <span class="bookshelf__status bookshelf__status--{{ status }}">{{ item.status | default: "Queued" }}</span>
    </div>
    <div class="bookshelf__meta">
      <h3 class="bookshelf__title">{{ item.title }}</h3>
      {% if item.author %}<p class="bookshelf__author">{{ item.author }}</p>{% endif %}
      {% if item.notes and item.notes != "" %}
        <div class="bookshelf__notes">{{ item.notes | markdownify }}</div>
      {% endif %}
    </div>
  </article>
{% endfor %}
</div>

{% endif %}
