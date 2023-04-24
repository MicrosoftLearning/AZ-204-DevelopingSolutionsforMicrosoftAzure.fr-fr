---
title: Instructions hébergées en ligne
permalink: index.html
layout: home
ms.openlocfilehash: 8cc220d44fe56f19385b25675c29e391b610db8e
ms.sourcegitcommit: d2d374fffa4fcbf92b9c4bdc9c9ecc470152e033
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/16/2021
ms.locfileid: "145196151"
---
## <a name="content-directory"></a>Répertoire de contenu

Les liens hypertexte vers chaque labo sont répertoriés ci-dessous.

## <a name="labs"></a>Laboratoires

{% assign labs = site.pages | where_exp: "page", "page.url contains '/Instructions/Labs'" %}
| Module | Laboratoire |
| --- | --- |
{% for activity in labs  %}{% if activity.lab.az204Module %}| {{ activity.lab.az204Module }} | [{{ activity.lab.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endif %}{% endfor %}

## Demos

## <a name="demos"></a>Démos

{% assign demos = site.pages | where_exp:"page", "page.url contains '/Instructions/Demos'" %}
| Module | Démo |
| --- | --- | 
{% for activity in demos  %}| {{ activity.demo.az204Module }} | [{{ activity.demo.az204Title }}]({{ site.github.url }}{{ activity.url }}) |
{% endfor %}
