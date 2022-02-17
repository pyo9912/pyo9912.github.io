---
title: "Git Issue"
layout: archive
permalink: categories/git
author_profile: false
sidebar_main: true
---

{% assign posts = site.categories.Git %}
{% for post in posts %}
    {% include custom-archive-single.html type=page.entries_layout %}
{% endfor %}