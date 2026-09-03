---
layout: page
title: News
permalink: /news/
nav: true
nav_order: 2
---

{% include news.liquid %}


<div class="news-filters" role="group" aria-label="Filter news by category">
  <button class="news-filter active" data-filter="all">
    <i class="fa-solid fa-layer-group"></i>
    ALL
  </button>

  <button class="news-filter filter-award" data-filter="award">
    <i class="fa-solid fa-award"></i>
    AWARD
  </button>

  <button class="news-filter filter-milestone" data-filter="milestone">
    <i class="fa-solid fa-flag-checkered"></i>
    MILESTONE
  </button>

  <button class="news-filter filter-paper" data-filter="paper">
    <i class="fa-solid fa-file-lines"></i>
    PAPER
  </button>

  <button class="news-filter filter-talk" data-filter="talk">
    <i class="fa-solid fa-microphone"></i>
    TALK
  </button>
</div>

{% assign sorted_news = site.news | sort: "date" | reverse %}

<div class="news-items">
  {% if sorted_news.size > 0 %}
    {% for item in sorted_news %}
      {% assign news_kind = item.kind | default: "milestone" | downcase %}

      <article
        class="news-item news-{{ news_kind }}"
        data-kind="{{ news_kind }}"
      >
        <div class="news-meta">
          <span class="news-badge">
            {% case news_kind %}
              {% when "award" %}
                <i class="fa-solid fa-award"></i>
              {% when "milestone" %}
                <i class="fa-solid fa-flag-checkered"></i>
              {% when "paper" %}
                <i class="fa-solid fa-file-lines"></i>
              {% when "talk" %}
                <i class="fa-solid fa-microphone"></i>
              {% else %}
                <i class="fa-solid fa-circle-info"></i>
            {% endcase %}

            {{ news_kind }}
          </span>

          <time datetime="{{ item.date | date_to_xmlschema }}">
            {{ item.date | date: "%b %Y" }}
          </time>
        </div>

        <div class="news-content">
          {{ item.content }}
        </div>
      </article>
    {% endfor %}
  {% else %}
    <p>No news so far...</p>
  {% endif %}
</div>

<style>
  /* Filter buttons */

  .news-filters {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.65rem;
    margin: 1.5rem 0 2rem;
  }

  .news-filter {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.42rem 0.85rem;
    border: 2px solid #8a8a8a;
    border-radius: 999px;
    background: transparent;
    color: var(--global-text-color);
    font-size: 0.85rem;
    font-weight: 700;
    letter-spacing: 0.035rem;
    line-height: 1;
    cursor: pointer;
    transition:
      background-color 0.2s ease,
      color 0.2s ease,
      transform 0.2s ease;
  }

  .news-filter:hover {
    transform: translateY(-1px);
  }

  .news-filter.active {
    border-color: #888;
    background: #888;
    color: #fff;
  }

  .news-filter.filter-award {
    border-color: #d43d3d;
  }

  .news-filter.filter-award.active {
    background: #d43d3d;
    color: #fff;
  }

  .news-filter.filter-milestone {
    border-color: #659c39;
  }

  .news-filter.filter-milestone.active {
    background: #659c39;
    color: #fff;
  }

  .news-filter.filter-paper {
    border-color: #248f87;
  }

  .news-filter.filter-paper.active {
    background: #248f87;
    color: #fff;
  }

  .news-filter.filter-talk {
    border-color: #c86519;
  }

  .news-filter.filter-talk.active {
    background: #c86519;
    color: #fff;
  }

  /* News rows */

  .news-items {
    width: 100%;
  }

  .news-item {
    position: relative;
    margin-bottom: 1.6rem;
    padding: 0 0 0.2rem 1.4rem;
  }

  .news-item::before {
    position: absolute;
    top: 0.2rem;
    bottom: 0;
    left: 0;
    width: 4px;
    border-radius: 999px;
    background: #888;
    content: "";
  }

  .news-item.news-award::before {
    background: #d43d3d;
  }

  .news-item.news-milestone::before {
    background: #659c39;
  }

  .news-item.news-paper::before {
    background: #248f87;
  }

  .news-item.news-talk::before {
    background: #c86519;
  }

  /* Badge and date */

  .news-meta {
    display: flex;
    flex-wrap: wrap;
    align-items: center;
    gap: 0.8rem;
    margin-bottom: 0.35rem;
  }

  .news-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    padding: 0.23rem 0.55rem;
    border: 1.5px solid #888;
    border-radius: 4px;
    color: #888;
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.05rem;
    line-height: 1;
    text-transform: uppercase;
  }

  .news-award .news-badge {
    border-color: #d43d3d;
    color: #d43d3d;
  }

  .news-milestone .news-badge {
    border-color: #659c39;
    color: #659c39;
  }

  .news-paper .news-badge {
    border-color: #248f87;
    color: #248f87;
  }

  .news-talk .news-badge {
    border-color: #c86519;
    color: #c86519;
  }

  .news-meta time {
    color: var(--global-text-color-light);
    font-size: 0.95rem;
    white-space: nowrap;
  }

  /* Announcement text */

  .news-content {
    color: var(--global-text-color);
    font-size: 1.05rem;
    line-height: 1.55;
  }

  .news-content p {
    margin: 0;
  }

  .news-content a {
    color: var(--global-theme-color);
  }

  /* Used by category filtering */

  .news-item.news-hidden {
    display: none;
  }

  @media (max-width: 600px) {
    .news-filters {
      gap: 0.5rem;
    }

    .news-filter {
      padding: 0.38rem 0.65rem;
      font-size: 0.75rem;
    }

    .news-item {
      padding-left: 1rem;
    }

    .news-content {
      font-size: 1rem;
    }
  }
</style>

<script>
  document.addEventListener("DOMContentLoaded", function () {
    const filterButtons = document.querySelectorAll(".news-filter");
    const newsItems = document.querySelectorAll(".news-item");

    filterButtons.forEach(function (button) {
      button.addEventListener("click", function () {
        const selectedKind = button.dataset.filter;

        filterButtons.forEach(function (otherButton) {
          otherButton.classList.remove("active");
        });

        button.classList.add("active");

        newsItems.forEach(function (item) {
          const itemKind = item.dataset.kind;
          const shouldShow =
            selectedKind === "all" || itemKind === selectedKind;

          item.classList.toggle("news-hidden", !shouldShow);
        });
      });
    });
  });
</script>
