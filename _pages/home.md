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

This site contains (at least should) all the necessary information about Git submodules.

## 1. Possible application

Let's start with sketching some example how someone can take advantage of git submodules. Assume that we are developing some website, and we are in the backend team responsible for the website structure which takes care of the whole appearance. It doesn't want to be involved in anything connected with working on the content. Having a widely extended website it would be a small challenge to accommodate the work of two groups, one mentioned and the second for content creation. All of those branches and subbranches to take care of. Why don't split this work into two repositories (site_repo, content_repo) and connect content_repo to the site_repo, arranging a fully functioning system? Site_repo would have one extra folder, whereas content_repo wouldn't have anything additional. No one from this team would have the possibility to mistakenly change something in some `.css` file and break half of the site structure.

This kind of combined workflow has been added to this site. If you click on the `Entertainment` bar in the top right corner, you will see some pages which haven't been created inside this repository, but in some other place in GitHub. However, it should be highlighted that in this case usage of git submodules was a form over substance. Trying to connect these two repos, and work on them simultaneously on one computer while hardworking on distinguishing high-quality memes was a bit annoying. Before starting to implement some new tool, one should always ask oneself if it is a good idea and make another minimal mistake.

<p align="center">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/sad_meme.png" alt="alt_text" width="600"/>
</p>

The question is, how one can create such functionality?

---

## 2. Submodule creation

### 2.1. Locally

Based on:

https://www.youtube.com/watch?v=RgIAXF53a8U&list=PL_RrEj88onS-jN7dZb-tYz0cpsxuA23Cm

### 2.2. Remotely