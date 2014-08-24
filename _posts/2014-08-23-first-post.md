---
layout: post
title:  "Customizing WordPress Archives For Categories, Tags And Other Taxonomies"
date:   2014-08-23 18:43:39
tags: user-experience
---

<p>Most WordPress users are familiar with tags and categories and with how to use them to organize their blog posts. If you use custom post types in WordPress, you might need to organize them like categories and tags. Categories and tags are examples of taxonomies, and WordPress allows you to create as many custom taxonomies as you want. These custom taxonomies operate like categories or tags, but are separate.</p>
<p>In this tutorial, we’ll explain custom taxonomies and how to create them. We’ll also go over which template files in a WordPress theme control the archives of built-in and custom taxonomies, and some advanced techniques for customizing the behavior of taxonomy archives.</p>
<p>Before continuing, let’s get our terminology straight. A taxonomy is a WordPress content type, used primarily to organize content of any other content type. The two taxonomies everyone is familiar with are built in: categories and tags. We tend to call an individual posting of a tag a “tag,” but to be precise, we should refer to it as a “term” in the “tag” taxonomy. We pretty much always refer to items in a custom taxonomy as “terms.”</p>
<p>Categories and tags represent the two types of taxonomies: hierarchical and non-hierarchical. Like categories, hierarchical taxonomies can have parent-child relationships between terms in the taxonomy. For example, you might have on your blog a “films” category that has several child categories, with names like “foreign” and “domestic.” Custom taxonomies may also be hierarchical, like categories, or non-hierarchical, like tags.</p>