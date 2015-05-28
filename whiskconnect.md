---
layout: page
title: WhiskConnect
permalink: /WhiskConnect/
---


WhiskConnect is a service that connects your online products to the Whisk Shopping List.

This document will describe everything you need to get your site WhiskConnected, and is aimed at developers wishing to integrate WhiskConnect into a website containing purchasable products.

Specifically, we will cover:

* TOC
{:toc}


# Adding the WhiskConnect script to your product page

In order to integrate WhiskConnect, you need to include a small piece of JavaScript on your page:

{% highlight html %}
<script async="true" src="//widget.whisk.com/assets/whiskbutton.js" type="text/javascript"></script>
{% endhighlight %}

We recommend you add this just before the closing `</body>` tag of your page (template), so that the script does not interfere with the usual page-loading process.

In fact, that's exactly what we've done on this page!


# Getting a WhiskConnect Owner ID

WhiskConnect can easily connect any text-based products to the Whisk Shopping List, but you are probably also interested in getting access to our analytics and dashboards.

In order for you to use Whisk Connect and get access to our dashboards and analytics, you first need to register with Whisk to become an "owner" of connected products. This allows us to group together all your products and analytic information so that you can track how your customers are using WhiskConnect.

At present, we're in a limited-access beta, and you need to manually register with us to use WhiskConnect. Don't worry - this is only temporary, and we'll automate the whole process soon enough. For now, if you'd like a WhiskConnect Owner ID, please [get in touch](hello@whisk.com)!

# WhiskConnect widget demos

In order to build a WhiskConnect widget, you

## A minimal example

The simplest possible example of a WhiskConnect widget needs only two HTML data attributes:

* `data-whisk-widget` to tell the WhiskConnect script that this is a widget
* `data-whisk-product-text="<your product here>"` to tell WhiskConnect what to add to the Whisk Shopping List.

Sounds easy? It is! Here's a simple HTML button enabled with WhiskConnect:

{% highlight html linenos %}
<button type="button" data-whisk-widget data-whisk-product-text="Almonds">
  A really simply button to add "Almonds" to Whisk
</button>
{% endhighlight %}

and here's how it looks in action:

<button type="button" data-whisk-widget data-whisk-product-text="Almonds">
  A really simply button to add "Almonds" to Whisk
</button>

### (Include your Owner ID as a data-attribute)

The above code assumes you've included your Owner ID in a `<meta>` tag elsewhere in the page. If you'd rather inline it directly into your widget, that's possible - you just need to include the `data-whisk-owner-id` attribute on your widget. This is how we would modify our earlier example:

{% highlight html linenos %}
<button type="button" data-whisk-widget data-whisk-product-text="Almonds"
    data-whisk-owner-id="d84ecba1-bfb1-4395-99f0-ae02910d4802">
  A really simply button to add "Almonds", with an Owner ID
</button>
{% endhighlight %}

## Styling your widget

The above example is fully functional, but it is not much to look at. Let's take a look at how to style your widgets for your site.

The data attributes described can be applied to any clickable HTML element, and you can style those elements however you want. This one has custom (inline) styles and an embedded ([Font Awesome](http://fortawesome.github.io/Font-Awesome/)) icon:

{% highlight html linenos %}
<a data-whisk-widget
    data-whisk-product-text="Biscuits"
    style="border-radius: 5px; border: 1px solid #777; color: white; background-color: red; padding: 1ex; cursor: pointer; display: inline-block;">
  <i class="fa fa-check-square"></i>
  A slightly nicer widget to add "Biscuits" to Whisk
</a>
{% endhighlight %}

and here's how it looks in action:

<a data-whisk-widget
    data-whisk-product-text="Biscuits"
    style="border-radius: 5px; border: 1px solid #777; color: white; background-color: red; padding: 1ex; cursor: pointer; display: inline-block;">
  <i class="fa fa-check-square"></i>
  A slightly nicer widget to add "Biscuits" to Whisk
</a>

Ok, so we're not going to win any design awards, but you get the idea.

## Widgets with nested buttons


The examples we've seen so far are very simple, and you're likely to want more control over the precise markup of your widget, including changing where the user has to click to add the product to the Whisk Shopping List.

There's an extra data attribute to give you flexibility over the click-target that opens the Whisk Shopping List: `data-whisk-action`.

By default, the element marked `data-whisk-widget` is a click target, and clicks anywhere inside it will add the chosen product to the Whisk Shopping List. If you'd rather separate the click target, you can add an element inside the Widget and give it the `data-whisk-action` attribute to make it the clickable target.

{% highlight html linenos %}
<div data-whisk-widget
    data-whisk-product-text="Chocolate"
    style="border-radius: 5px; border: 1px solid #777; color: #333; background-color: #ddd; padding: 1em;">
  We really want you to add
  <a data-whisk-action style="border-radius: 5px; background-color: brown; color: white; cursor: pointer; padding: 1ex; margin: 1ex; whitespace: no-wrap;">
    <i class="fa fa-check-square"></i> Chocolate
  </a>
  to your Whisk Shopping List, but just had to tell you some more about it, and it takes up so much space, and <i>OH MY!</i>.
</div>
{% endhighlight %}

Once again, here's how it looks:

<div data-whisk-widget
    data-whisk-product-text="Chocolate"
    style="border-radius: 5px; border: 1px solid #777; color: #333; background-color: #ddd; padding: 1em;">
  We really want you to add:
  <a data-whisk-action style="border-radius: 5px; background-color: brown; color: white; cursor: pointer; padding: 1ex; margin: 1ex; whitespace: no-wrap;">
    <i class="fa fa-check-square"></i> Chocolate
  </a>
  to your Whisk Shopping List, but just had to tell you some more about it, and it takes up so much space, and <i>OH MY!</i>.
</div>



## Changing Whisk behaviour with <i>Actions</i>


# Using WhiskConnect in non-English languages

By default, WhiskConnect assumes your products are written in English, but we at Whisk love all languages... we're just a bit time-limited.

We support a number of other languages, and you can specify the language of a product widget by including the `data-whisk-language` attribute, and specifying a language code. Here are a few examples:

The list of supported languages at present is:

<table>
  <thead>
    <tr><th>Language</th><th>Code</th></tr>
  </thead>
  <tbody>
    <tr><td>English</td><td>en</td></tr>
    <tr><td>English (GB)</td><td>en-gb</td></tr>
    <tr><td>English (US)</td><td>en-us</td></tr>
    <tr><td>French</td><td>fr</td></tr>
    <tr><td>French (Quebec)</td><td>fr-qc</td></tr>
    <tr><td>German</td><td>de</td></tr>
    <tr><td>Polish</td><td>pl</td></tr>
    <tr><td>Spanish</td><td>es</td></tr>
    <tr><td>Spanish (Argentinian)</td><td>es-ar</td></tr>
    <tr><td>Spanish (Mexican)</td><td>es-mx</td></tr>
  </tbody>
</table>

<script async="true" src="//widget.whisk.com/assets/whiskbutton.js" type="text/javascript"></script>
