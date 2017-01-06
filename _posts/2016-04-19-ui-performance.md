---
layout: post
title:  "UI Performance"
date:   2016-04-19 12:00:00
tags: html css
---

In my [last blog post](http://grigoria.gr/2015/05/11/users-have-time.html), I mentioned that there is a high probability of a user to leave a website in the first 10 seconds. Things nowadays move fast and in the online world, things move faster. Recent studies have proven that human now has shorter attention span than goldfishes, due to digital technology. Users don't want (and won't) spend time with you.

You may want to improve your website's usability or add new features to increase user engagement. The truth is that the most important step in designing for user experience is to improve website performance. While designing your website's UX, first make it fast. If you can do this with no cost in design, then...good for you.

One of the most important things that I have learned while working on large-scale websites is that performance starts from UI. Designers should care about website performance, engineers should care about usability. It is an ongoing process that results in improving user experience. Performance is a general subject with many branches, so I won't cover everything. These are just some simple things I consider as best practices:

#### HTML
Keep your HTML as short as it needs to be. Use **no more elements than you need** and **avoid using id/class** if you don't need them. That said, avoid **many inline SVG** as they increase HTML bloat and **don't use comments** in HTML. If it's possible, add them using backend template language, so that they are not added to the DOM.

For example, in a Rails project, I would use this to prevent comments from appearing in the DOM:

{% highlight css %}
    <%# This is a comment that you won't see in the DOM %>

    <header>
        ...
    </header>

    instead of this:

    <!-- This is a ------HEADER----- and a useless comment since you already see the word header in the tag -->

    <header>
        ...
    </header>
{% endhighlight %}


The code is still well documented.

There will be times where you will have to increase the HTML size rather than do an extra request. Do the math or follow your heart.

#### CSS
Make your code **as [DRY](http://www.slideshare.net/jeremyclarke/dry-css-a-dontrepeatyourself-methodology-for-creating-efficient-unified-and-scalable-stylesheets) as possible**. You can do this by using a CSS preprocessor or by using methodologies like OOCSS, SMACSS or BEM. (Using a preprocessor won’t really help you increase website’s performance, but it will help you in writing “DRY" code.) Whatever you do, make sure that you don't repeat yourself.

Be sure to delete styles that you no longer use and be sure that you **load just the styles that you are going to use**. Following a **mobile-first** approach in development (if done right) will help you do this. Begin building things for mobile and continue adding styles for larger viewports, rather than loading everything in the mobile and just display: none them. Styles will still be loaded and in [some cases](https://timkadlec.com/2012/04/media-query-asset-downloading-results/), assets will be downloaded even if you hide them with display: none.

**Avoid using id or high specificity.** Beyond all doubt,  you can't write DRY code using selectors with high specificity. It is most likely that a few lines below, you are going to override the rules. Moreover, (quoting Harry Roberts) by using something like
`html body .header .nav{}`
the browser has to look out for four things, the `.nav` class, then the `.header` class, then the body element and then, finally, the html element. Use something like `.nav {}` instead. I suggest reading Harry Roberts' article about how to "[Keep your CSS selectors short](http://csswizardry.com/2012/05/keep-your-css-selectors-short/)".

**Structure your CSS files** in a way that you load just the styles that you need. It's a good idea to split your files and load each one when needed. If you build a website and its admin panel, you can split the CSS files in application.css and admin.css.

Finally, **don't use CSS rules that increase paint time**. For example, avoid using the old `text-indent: -99999999px` and use Zeldman's [image replacement](http://www.zeldman.com/2012/03/01/replacing-the-9999px-hack-new-image-replacement/) technique. Furthermore, by using certain CSS rules,  you can trick the browser into triggering GPU acceleration. So, it's a good technique to apply transform: translateZ in elements that are in a fixed position or to animate elements ([Read more](http://blog.teamtreehouse.com/increase-your-sites-performance-with-hardware-accelerated-css) about Hardware-accelerated CSS). CSS properties like box-shadow [affect](http://www.html5rocks.com/en/tutorials/speed/css-paint-times/) your page paint time, too.

#### Images
The maximum parallel HTTP connections per server are in average 6 (the number differs for every browser).
Once again: Use as fewer images as possible because they cost. They cost connections and in the case of mobile users, images cost them data usage which they pay for.

What would I do to decrease the number of images:

1. I would use just the necessary images in mobile views.
2. I wouldn't add retina support for images where quality doesn’t matter. Personally, I just add retina support for icons.
3. If I can do something with simple CSS, I do it and I avoid using an image. Using images for gradients, arrows and this kind of stuff is "très passé”.
4. Old good sprite can be handful when you have to load a lot of images in CSS. Loading each image every time you need it is harmful performance-wise (in HTTP1.1). In the case of SVG, you can create an image sprite using the [SVG stacking](https://hofmannsven.com/2013/laboratory/svg-stacking/) method.

Another tactic I usually follow is using data-URI for small icons. Data-URI are 33% larger than images in CSS and browser doesn't cache them.
According to a [research](http://www.mobify.com/blog/css-sprites-vs-data-uris-which-is-faster-on-mobile/), it is recommended that we should _"limit the use of data URIs to very small resources and to not use too many of them in the CSS or inline HTML. 15-20kB for max data URI size, and no more than 3 - 5 instances seems like a good rule of thumb for mobile"_ . Despite that, data-URI is a useful way to embed small items of data into a URL, rather than link to an external resource, to avoid the cost of extra request.

Before all that, images have to be optimized for minimum size. I usually set to myself the limit to 60-70kb per image but of course, this isn’t a general rule. This is a random number and it depends on the quality I need to have each time.

The tools I use to optimize images:

* Adobe’s Photoshop for **JPG**: Save them for web in the lowest decent quality and be sure to save them to be “progressive”.
* [ImageAlpha](https://pngmini.com/) for **PNG** format
* [SVGO-GUI](https://github.com/svg/svgo-gui) tool minifies **SVG** files up to 50-60%

#### Fonts
Same for images, use as fewer fonts as possible and as fewer character sets as possible. If you plan to use bold for just one element, avoid to load the whole font-weight. I support the ["Don't fake styles"](https://twitter.com/grigoriap/status/424842509228179456) rule, but if I have to choose performance or design, I vote for performance. Avoid loading a whole font to render just a few icons. In the case of fewer than 10-15 icons I use a sprite or inline SVG instead of icon fonts, to avoid the cost of the extra request.

Currently, we can use fonts that we self-host or import them into websites by using an external service like Google fonts, Typekit etc. Also, we can import a font by adding a script in the HTML.

For example:

```
    <script type="text/javascript" src="//fast.fonts.net/jsapi/6665ec77-7ab3-4d6d-859f-b85c03408141.js"></script>
```

or using the CSS way:

```
    <link type="text/css" rel="stylesheet" href="//fast.fonts.net/cssapi/6665ec77-7ab3-4d6d-859f-b85c03408141.css”/> 
```

or


```
  @import url(http://fonts.googleapis.com/css?family=Oswald:300);
```

`<link>` is preferred to `@import`, as it doesn't block parallel downloads.

The answer to the question "Which one of these methods should I use?" is again: "It depends". Or at least, I don't know. Most services, as Google fonts, Typekit and Fonts.com have done a lot of performance optimizations&#x2a; in the way they serve fonts. Therefore, in many cases importing a font asynchronously is a good idea performance-wise. You can even avoid FOUC, so... why not? Sometimes it is better to use the self-hosted way: the servers location or caching the font are just two of the reasons why you should. So again, there isn't a unique solution. Do your research and select the most suitable way.

Lea Verou has recently tweeted:

<div class="embed-tweet">
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Any HTML/CSS course should start with an intro to dev tools. Unbelievable there are still people who don’t know how to inspect an element.</p>&mdash; Lea Verou (@LeaVerou) <a href="https://twitter.com/LeaVerou/status/710920718544998400">March 18, 2016</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>


We, designengineers, usually inspect an element, but rarely inspect the network or timeline to see the impact of their changes. As we don't only affect the styles but performance too, we should care equally about it. So, while you inspect your element, be sure to check the network tab once in a while.

&#x2a; Read more:

  * [Web Font Loader](https://github.com/typekit/webfontloader)
  * [Optimizing your font requests](https://developers.google.com/fonts/docs/getting_started#optimizing_your_font_requests_beta)
  * [New Improvements to Dynamic](http://blog.fonts.com/2015/05/new-improvements-to-dynamic-subsetting/)
