---
layout: post
title:  "Four selectors and a mixin"
date:   2014-10-14 10:37:39
tags: css
---

<p>Selectors offer a lot of flexibility and (if used correctly) may reduce many lines of code, such as overrides.
<br />
The following are not my favorite selectors; I'm not so nerd to have favorite selectors. They are some that, even if I don't use them very often, I find useful and sometimes can save you from the trouble of inventing proper class names.</p>

#### X:not()

Use `:not` when you want to select all elements except one. So, instead of applying general rules and then overriding them, like:

{% highlight css %}
X {
  padding-bottom: 20px;
  border-bottom: 1px solid black;
}

X:last-child {
  padding-bottom: 0;
  border-bottom: none;
}
{% endhighlight %}

you can use `:not`:

{% highlight css %}
X:not(:last-child) {
  padding-bottom: 20px;
  border-bottom: 1px solid black;
}
{% endhighlight %}

#### X + *

I usually use this one to clear floats but I find it very versatile. What it basically does is select whatever is right after the given element.

For example:

{% highlight css %}
X {
  float: left;
}

X + * {
  clear: left;
}
{% endhighlight %}

#### X:nth-child(odd/even)


`nth-child(N)` accepts an integer (N) as a parameter and targets the nth list item.

Instead of an integer, nth-child also accepts two keywords: even and odd. "Even" selects even elements, like the 2nd, 4th, 6th, etc. "Odd" selects odd elements, like 1st, 3rd, 5th, etc.

It can be especially useful in a, let's say, 2-column layout where you want to select only the elements of the second column.

For example:

{% highlight css %}
li {
  float: left;
  margin-right: 40px;
}

li:nth-child(even) {
  margin-right 0;
}
{% endhighlight %}

#### X:nth-last-child(Ν)

This one selects the nth to last element.

For example, the following lines apply green color to the second to last li:

{% highlight css %}
li:nth-last-child(2) {
  color: green;
}
{% endhighlight %}

####  Mixin for not applying hover effect on touch screen devices

This is a mixin I created with my fellow and sass fanboy, <a href="http://vangeltzo.com/" target="_blank">vangeltzo</a>, when we didn't want hover states in mobile views so as to avoid useless browser painting. This mixin applies hover state to the elements for viewports larger than 960px. In IE8, which doesn't support media queries, the elements will have hover state in all viewports. Eventually we didn't use it because it increases code complexity in large projects.

Another reason for not using this mixin is that <a href="http://msdn.microsoft.com/en-us/library/ie/dn265029(v=vs.85).aspx" target="_blank">IE11 supports hover touch</a>, while IE7 doesn't have a hover state at all.

There is <a href="http://stackoverflow.com/questions/2741816/is-it-possible-to-force-ignore-the-hover-pseudoclass-for-iphone-ipad-users" target="_blank">another suggestion</a> for removing hover states from touch devices, that I also find very messy.

{% highlight css %}
@mixin hover {

  @media only screen and (min-device-width: 960px) {
    &:hover {
      @content;
    }
  }

  @at-root .ie8 & {

    &:hover {
      @content;
    }
  }
}
{% endhighlight %}
