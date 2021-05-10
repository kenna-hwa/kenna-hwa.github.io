---
layout: section
title: blog
permalink: /blog
---
{% include sections/last_post.html last_post=site.blog.last%}
{% include sections/items_except_last.html items=site.blog%}
