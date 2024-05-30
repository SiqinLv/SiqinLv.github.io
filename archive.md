---
layout: page
title: Blog Archive
---

<div class="container">
    {% for tag in site.tags %}
      <h3>{{ tag[0] }}</h3>
      <ul>
        {% for post in tag[1] %}
          <li><a href="{{ post.url }}">{{ post.date | date: "%B %Y" }} - {{ post.title }}</a></li>
        {% endfor %}
      </ul>
    {% endfor %}
</div>

<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #f8f8f8;
        color: #333;
        margin: 0;
        padding: 20px;
        line-height: 1.6;
    }
    .container {
        max-width: 800px;
        margin: auto;
        padding: 20px;
        background-color: #fff;
        box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        border-radius: 8px;
    }
    h1 {
        text-align: center;
        color: #007BFF;
    }
    h3 {
        margin-top: 20px;
        color: #007BFF;
    }
    ul {
        list-style: none;
        padding: 0;
    }
    li {
        margin: 10px 0;
        padding: 10px;
        background-color: #f1f1f1;
        border-left: 4px solid #007BFF;
        transition: background-color 0.3s ease;
    }
    li:hover {
        background-color: #e1e1e1;
    }
    a {
        text-decoration: none;
        color: #333;
        font-weight: bold;
        transition: color 0.3s ease;
    }
    a:hover {
        color: #007BFF;
    }
</style>
