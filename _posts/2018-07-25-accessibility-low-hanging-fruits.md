---
layout: post
title:  "Accessibility low hanging fruit"
date:   2018-08-25 09:00:00
tags: accessibility ux html
---

User experience is most commonly associated with any human-computer interaction and it is used to describe the way people react to a system. We build things for people, so how they experience their interaction with these things is maybe what matters most.

User experience is strongly connected with Web accessibility. Web accessibility is making products and services available to all users, regardless of their physical ability, internet speed, or the device they are using.

Accessibility is very often sidelined due to the small percentage of users suffering from a permanent disability. But making a product more accessible has a very strong impact on how all users are able to interact with it.

Making a Website accessible have different levels and depths. In this blog post, you’ll find what I consider accessibility’s “low hanging fruit”.

By following basic guidelines, you can improve a Website’s accessibility with simple steps.

### Design

UI designer is almost always correlated with UX design. People designing for the Web have always in mind designing for user experience. That means that they should have in mind, not only the standard rules of design but also accessibility rules.

#### Contrast ratio

The term contrast ratio in Web is usually used to describe the contrast of the text or foreground compared to the background. Having a low contrast ratio may result in people not being able to distinguish the foreground or, even worse, the text. Keep in mind that not everyone has a good screen and not everyone has good vision. There are various tools for the Web built to check the contrast ratio between background and text:

[https://Webaim.org/resources/contrastchecker/](https://Webaim.org/resources/contrastchecker/)
[http://leaverou.github.io/contrast-ratio/](http://leaverou.github.io/contrast-ratio/)

#### Animations

Using quick animations may be really disturbing for many people, especially those with brain dysfunctions. Also, blinking text and moving text can distract the reader's attention, so avoid using them.

#### Hover actions

Hover actions is a good example of how users without a disability have benefit by accessible designs. Until recently, using action on mouse-over was avoided because hover is an action inaccessible on mobiles. Not using actions on mouse-over also help people that can’t use a mouse or their hand effectively. Instead, use a button that can trigger a popover or window easily accessible by keyboard, too.

### Text

#### Zoom

WCAG 2.0 Level AA, Guideline 1.4.4 speaks to the importance of letting the user resize text:

> Except for captions and images of text, text can be resized without assistive technology up to 200 percent without loss of content or functionality.

This guideline states that all Website text must be resizable (zoomable).

The more relevant portion of this guideline is for touch displays and pinch-zooming behaviors. Adding the following in the `<head>` will disabled zooming:

`<meta name="viewport" content="width=device-width, initial-scale=1.0,
maximum-scale=1.0, user-scalable=no" />`

Zooming is commonly disabled for design reasons, but this should be avoided as it removes functionality from the users who want to see enlarged text.

Users with low vision often alter the settings of their browsers to accommodate their needs, so it is important that your design accommodate increased text sizes without loss of readability or functionality. Therefore, it is best to use relative units to specify font sizes rather than absolute units. Users should be able to see enlarged text when they change the default font size in their browser.

#### Contrast ratio

As noted before, the Web Content Accessibility Guidelines define a formula for determining whether there is sufficient contrast between the foreground and the background. Text is much easier to read when there is a sufficient contrast between the text and the background. Tools such as WebAIM's Color Contrast Checkermake it easy to check contrast thresholds and determine Web Content Accessibility Guidelines compliance.

### Markup

As a general rule of thumb, accessibility works until you break it. That means that by following the Web standards and by having a well structured and semantically correct markup, we follow the basic accessibility rules.

#### Page elements

##### Semantically correct markup

Replace meaningless `<div>`s with more meaningful elements where appropriate. Screen readers read elements from HTML and behave differently. Semantic HTML gives context to screen readers, which read the contents of a Web page out loud. (Read here how each screen reader speaks different elements.).
Also, avoid reordering with `float: right` because it changes the flow of screen readers and in some cases it makes to sense. Same for reordering with flexbox’s `order` rule.

##### Page title

A page title is a short title which is unique for each Web page and describes the page content. This is helpful for all users, but is especially helpful for blind users, as the title is typically announced by screen readers as soon as a new page is loaded in the Web browser or a new document is loaded in the reading application.

##### Images

Every `<img>` tag should contain an `<alt>` attribute which describes the information or function of the image. The alt tag is used by screen readers to tell blind and visually impaired people what is on the image, so it has to be descriptive and informative of the action/purpose. For example, in the case of an image button which is used as a link to buy product X, the alternate text should be something like “Buy product X now for $19!”.

For purely decorative images, there is no need to write alternative text. The empty alt attribute makes sure that screen readers skip over the image. This is something that I wouldn’t recommend, though. When possible, decorative images should be in your CSS and not in your HTML.

##### Links

Following the first rule about semantically correct markup, use a link when it is actually a link to another page or another section. Don’t use a link with events on it, because semantically, this is a button, not a `<a href=’#’ onClick=’...’>`
Screen readers read links as “links” so you don’t need to add the word “Link to…” or “Goes to...” in the link title. Use the link title to help the user understand what the link is about, so make it meaningful. Avoid using ambiguous link text, such as 'click here' or 'read more' and don’t use the same title and text because screen readers read it twice.

##### Headings

Section headings are used to organize the content and convey meaning and structure. The structure should be portrayed both in a visual and technical manner, so people can see the structure, and screen readers are able to identify the structure in order to read it out. adding headings is one of the most important ways a screen reader user can use to know what is on the page. So, headings should be descriptive in order to help users find specific content and orient themselves within the Web page.

##### Forms

To create an accessible online form, you must ensure that all form fields have accurate labels or prompt so screen reader users know what each field is asking for. Sighted users should be able to visually associate a text label with its corresponding form control. Users with visual disabilities, however, cannot make this visual association but labels can be associated programmatically with form controls using HTML markup. So, every input has to have a label and every label should refer to a unique input.

For example:

{% highlight css %}
  <div>
    <label for="name">First name</label>
    <input id="name" type="text" />
  </div>
{% endhighlight %}

If you find yourself tempted to use a label for two different inputs, use a `<legend>` instead. For example,

{% highlight css %}
  <fieldset>
    <legend>Work experience</legend>
    <label class=”sr-only”>From</label>
    <input type=”date” />
    <label class=”sr-only”>To</label>
    <input type=”date” />
  </fieldset>
{% endhighlight %}

where class `.sr-only` hides the content visually but allows screen readers to read it.

#### Keyboard navigation

##### Tabindex

A few words about tabindex: The tabindex attribute defines the navigation order for focusable elements (typically links and form controls) within a page. It can also be used to define whether elements should be focusable or not.

The tabindex attribute has three uses:

* `tabindex="1"` (or any number greater than 1) defines an explicit tab order.
* `tabindex="0"` allows elements to receive keyboard focus. It does not change the tab order, but places the element in the navigation flow, as if it were a link.
* `tabindex="-1"` removes the element from the default navigation flow and also allows it to receive programmatic focus. This may be useful for elements that should not be navigated to, but need to have the focus set to them. A good example is a modal dialog window: when opened, the focus should be set to the dialog so a screen reader will begin reading and the keyboard will be able to navigate within the dialog. Because the dialog (probably a `<div>` element) is not focusable by default, assigning it tabindex="-1" allows scripting to set focus to it when it is presented.

So, by explicitly changing the tabindex attribute of an item, we change the navigation order, which is generally a bad practice and should be avoided. If you find yourself want to use positive tabindex to rearrange the navigation order, then there is a high chance that you should change the markup instead. Negative tabindex should be avoided too, as it removes the element from the default navigation flow.

##### Semantic markup (again)

I won’t say much here as it’s mentioned before. Use semantically correct markup in order to allow keyboard navigation. There is a common mispractice where javascript events are added in divs/spans elements to fake a button effect. For example:

`<span class=”fake-link” onclick="hide()">Hide me</span>`

This may work on mouse click, but it’s not accessible with a keyboard or read by screen readers.

##### Accesskey

Keyboard shortcuts are a standard accessibility feature of most operating systems. Keyboard shortcuts can be useful to all computer users because they often allow for interactions that are faster than allowed by mouse clicks. "Power users" of all abilities frequently use keyboard shortcuts.
The accesskey HTML attribute allows Web developers to assign certain keyboard shortcuts to Web elements. Starting with HTML 4.0, the accesskey attribute can be added to interactive HTML elements, such as links and form controls. For example:

{% highlight css %}
<a href="https://www.google.com" accesskey="g">Google</a>
<a href="https://www.amazon.com" accesskey="a">Amazon</a>
{% endhighlight %}

One of the biggest problems with accesskey shortcuts is that users are not generally aware that they even exist. There are some ways to notify users that the accesskey shortcuts are available, but the truth is that, due to numerous problems with implementation, many developers choose to avoid them entirely.

### Aria attribute and roles

WAI-ARIA is a technology that can add further semantics that browsers and assistive technologies can recognize and use to let users know what is going on. WAI-ARIA is a specification written by the W3C, defining a set of additional HTML attributes that can be applied to elements to provide additional semantics and improve accessibility.

There are three main features defined in the spec:
Roles describe the type of widget presented, such as “menu,” “navitem,” “slider” or the structure of the Web page, such as headings and regions (ex. `role="navigation"` or `role="complementary"`). Properties define properties of elements, which can be used to give them extra meaning or semantics.
For example, `aria-required="true"` specifies that a form input needs to be filled in to be valid.
States describe the state widgets are in, such as “checked” for a checkbox, or “disabled” for a button.
ex. `<a aria-expanded="true"><div role="checkbox" aria-checked="true"`

I don’t really consider ARIA an accessibility low hanging fruit, so I won’t go into much detail. There are many possibilities there, and in order to be implemented correctly, requires some more reading. You can begin with the following links which I find very useful:

[https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
[https://www.w3.org/TR/html-aria/#allowed-aria-roles-states-and-properties](https://www.w3.org/TR/html-aria/#allowed-aria-roles-states-and-properties)
