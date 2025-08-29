---
title: Instrucciones del ejercicio
permalink: index.html
layout: home
---

# Ejercicios de GitHub Copilot

Los siguientes ejercicios de inicio rápido están diseñados para proporcionarle una experiencia práctica de aprendizaje en la que explorará las funcionalidades de GitHub Copilot. Cada ejercicio incluye un conjunto de tareas que puede completar en el entorno de laboratorio.

## Ejercicios de inicio rápido
<hr>

{% assign labs = site.pages | where_exp:"page", "page.url contains '/Instructions/Labs'" %}

{% for activity in labs  %}

### [{{ activity.lab.title }}]({{ site.github.url }}{{ activity.url }})
{{ activity.lab.description }}
<hr>
{% endfor %}
