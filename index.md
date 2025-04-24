---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
---

## Répertoire de contenu

Les liens hypertexte vers chaque labo sont répertoriés ci-dessous.

## Ateliers

{% assign labs = site.pages | where_exp: "page", "page.url contains '/Instructions/Labs'" %}
| Module | Laboratoire |
| --- | --- |
{% for activity in labs  %}{% if activity.lab.az204Module %}| {{ activity.lab.az204Module }} | [{{ activity.lab.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endif %}{% endfor %}

