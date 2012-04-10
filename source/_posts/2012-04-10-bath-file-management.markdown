---
layout: post
title: "Bath File Management"
date: 2012-04-10 23:31
comments: true
categories: 
- Cmd
- Script
---

### Batch Rename

    for i in *.png; do mv -i "$i" "PrefixWord$i"; done
