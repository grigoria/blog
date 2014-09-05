---
layout: post
title:  "Animating Without jQuery"
date:   2014-09-05 23:57:39
tags: user-experience design
---

<p>Reality check: JavaScript-based animation is often as fast as CSS-based animation — sometimes even faster. CSS animation only appears to have a leg up because it’s typically compared to jQuery’s $.animate(), which is, in fact, very slow. However, JavaScript animation libraries that bypass jQuery deliver incredible performance by avoiding DOM manipulation as much as possible. These libraries can be up to 20 times faster than jQuery.</p>
<p>CSS animations are convenient when you need to sprinkle property transitions into your style sheets. Plus, they deliver fantastic performance out of the box — without your having to add libraries to the page. However, when you use CSS transitions to power rich motion design (the kind you see in the latest versions of iOS and Android), they become too difficult to manage or their features simply fall short.</p>
<p>Before continuing, let’s get our terminology straight. A taxonomy is a WordPress content type, used primarily to organize content of any other content type. The two taxonomies everyone is familiar with are built in: categories and tags. We tend to call an individual posting of a tag a “tag,” but to be precise, we should refer to it as a “term” in the “tag” taxonomy. We pretty much always refer to items in a custom taxonomy as “terms.”</p>
<p>Categories and tags represent the two types of taxonomies: hierarchical and non-hierarchical. Like categories, hierarchical taxonomies can have parent-child relationships between terms in the taxonomy. For example, you might have on your blog a “films” category that has several child categories, with names like “foreign” and “domestic.” Custom taxonomies may also be hierarchical, like categories, or non-hierarchical, like tags.</p>