---
title: "Git Flow"
layout: archive
permalink: categories/gitflow
author_profile: false
sidebar_main: true
---

{% assign posts = site.categories.GitFlow %}
{% for post in posts %}
    {% include custom-archive-single.html type=page.entries_layout %}
{% endfor %}