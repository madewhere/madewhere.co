---
title: "{{ replace .Name "-" " " | title }}"
description:
date: {{ .Date }}

stub: true
draft: true

categories:
origins:
tags:
# set "parent" to the name of another brand
parent:
# or: set "parentLink" to link to an external site, but do not set both
parentLink:
  url:
  text:
vendors:

links:
  - url: https://brand.example/
    text: "{{ replace .Name "-" " " | title }}"
---
