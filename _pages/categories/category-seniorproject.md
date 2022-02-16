---
title: "졸업 프로젝트"
layout: archive
permalink: categories/seniorproject
author_profile: false
sidebar_main: true
---

{% assign posts = site.categories.SeniorProject %}
{% for post in posts %}
    {% include custom-archive-single.html type=page.entries_layout %}
{% endfor %}