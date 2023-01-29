---
layout: single
title: ""
permalink: /
toc: True
toc_label: "Table of contents"
toc_icon: "fas fa-list-ul"
toc_sticky: true
---

<span style="font-size:xx-large;">**How to work with submodules?**</span>

This site contains all the necessary information (available till 26th October) about Git submodules. It was based on [Git Pro - Submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules) and a moderate dose of Stackoverflow. It is assumed that the reader knows basics of Git. If not, [here](https://martinhronec.github.io/JEM224/) is an introduction.

## 1. Possible application

Before dealing with some definitions and other theoretical stuff, let's start with sketching an example of how someone can take advantage of git submodules. Assume that we are developing some websites and are in the backend team responsible for the website workflow and structure. The team doesn't want to be involved in anything connected with working on the content. Having a widely extended website, it would be a challenge to arrange the work of two groups, one mentioned and the second responsible for content creation. All those branches and subbranches to take care of. Why don't split this work into two repositories (site_repo, content_repo) and connect content_repo to the site_repo, arranging a fully functioning system? Site_repo would have one extra folder from which content would be taken, whereas content_repo wouldn't have anything additional. No one from this team would have the possibility of mistakenly changing something in some `.css` file and breaking half of the site functionality.

This kind of combined workflow has been added to this site. If you click on the `Entertainment` bar in the top right corner, you will see pages which haven't been created inside [this repository](https://github.com/wisniewski-mateusz/submodulesIES), but in [another](https://github.com/wisniewski-mateusz/submodulesIES_entertainment). However, it should be highlighted, that in this case, usage of git submodules was a form over substance. Connecting these two repos and working on them simultaneously on one computer while choosing high-quality memes was annoying. Before starting to implement some new tool, one should always ask oneself if it is a good idea and then make another minimal mistake. [^1]

<p align="center">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/sad_meme.png" alt="alt_text" width="600"/>
</p>

The question is, how this kind of functionality can be created? Before answering this question, let's catch up on some concepts.

## 2. Submodule creation

### 2.1. Locally

Based on:

https://www.youtube.com/watch?v=RgIAXF53a8U&list=PL_RrEj88onS-jN7dZb-tYz0cpsxuA23Cm

---

### 2.2. Remotely

---
---

[^1]: A small (minimal?) pun, since website is powered by [minimal mistakes](https://mademistakes.com/work/minimal-mistakes-jekyll-theme/).