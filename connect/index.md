---
layout: page
title: WhiskConnect
permalink: /connect/
---

WhiskConnect is a service that connects your online products to the Whisk Shopping List. You can find more details about WhiskConnect on our [marketing pages](https://whisk.com/connect/).

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

## Adding your Owner ID to the page

In order to correlate your products with your Owner ID, you must embed your Owner ID in each product page.  There are two ways to do this:

0. Using a single meta tag on the page
0. Adding a data-attribute to each Whisk widget

We'll cover the latter case [below](#including-your-owner-id-as-a-widget-data-attribute), after we've seen how to create a Whisk widget.

### Adding your Owner ID as a `<meta>` tag

The simplest way to add your Owner ID to your page is as a `<meta>` tag, usually situated inside the `<head>` of your page.  Assuming your Owner ID is `"d84ecba1-bfb1-4395-99f0-ae02910d4802"`, your `<meta>` tag would look like this:

{% highlight html %}
<meta name="whisk-owner-id" content="d84ecba1-bfb1-4395-99f0-ae02910d4802">
{% endhighlight %}


# Creating WhiskConnect widgets

In order to build a WhiskConnect widget, you need to add some markup to your page, to create a clickable element that is recognised by WhiskConnect's scripts.

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

### Including your Owner ID as a widget data-attribute

The above code assumes you've included your Owner ID in a `<meta>` tag elsewhere in the page. If you'd rather inline it directly into your widget, that's possible - you just need to include the `data-whisk-owner-id` attribute on your widget. This is how we would modify our earlier example:

{% highlight html linenos %}
<button type="button"
    data-whisk-widget
    data-whisk-product-text="Almonds"
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
    class="demo_widget red">
  <i class="fa fa-check-square"></i>
  A slightly nicer widget to add "Biscuits" to Whisk
</a>
{% endhighlight %}

and here's a live example:

<a data-whisk-widget
    data-whisk-product-text="Biscuits"
    class="demo_widget red">
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
    class="demo_widget_wrapper">
  We really want you to add
  <a data-whisk-action class="demo_widget brown">
    <i class="fa fa-check-square"></i> Chocolate
  </a>
  to your Whisk Shopping List, but just had to tell you some more about it, and it takes up so much space, and <i>OH MY!</i>.
</div>
{% endhighlight %}

Here's how it looks:

<div data-whisk-widget
    data-whisk-product-text="Chocolate"
    class="demo_widget_wrapper">
  We really want you to add:
  <a data-whisk-action class="demo_widget brown">
    <i class="fa fa-check-square"></i> Chocolate
  </a>
  to your Whisk Shopping List, but just had to tell you some more about it, and it takes up so much space, and <i>OH MY!</i>.
</div>



## Changing Whisk behaviour with <i>Actions</i>

Nesting buttons inside Whisk widgets may appear contrived, but there is a specific use case where it excels.

All previous examples have added the specified product to their Whisk Shopping List. This is a common action, but the users of your site will also want to get back to their Whisk Shopping List without adding new items.

This can be achieved using `data-whisk-action`, and specifying a value for the action. Valid action values are:

<table>
  <thead>
    <tr><th><code>data-whisk-action</code></th><th>Code</th></tr>
  </thead>
  <tbody>
    <tr><td><code>add_product_to_list</code></td><td>Adds the product to the Whisk Shopping List</td></tr>
    <tr><td><code>view_list</code></td><td>Views the current Whisk Shopping List</td></tr>
    <tr><td>(none)</td><td>Defaults to `add_product_to_list</code></td></tr>
  </tbody>
</table>

### A widget to view the Whisk Shopping List

The simplest possible Whisk widget provides the ability for the user to view their Whisk Shopping List:

{% highlight html linenos %}
<button type="button" data-whisk-widget data-whisk-product-text data-whisk-action="view_list">
  View Whisk Shopping List
</button>
{% endhighlight %}

Here it is:

<button type="button" data-whisk-widget data-whisk-product-text data-whisk-action="view_list">
  View Whisk Shopping List
</button>


### A Widget with multiple actions



The examples we've seen so far are very simple, and you're likely to want more control over the precise markup of your widget, including changing where the user has to click to add the product to the Whisk Shopping List.

There's an extra data attribute to give you flexibility over the click-target that opens the Whisk Shopping List: `data-whisk-action`.

By default, the element marked `data-whisk-widget` is a click target, and clicks anywhere inside it will add the chosen product to the Whisk Shopping List. If you'd rather separate the click target, you can add an element inside the Widget and give it the `data-whisk-action` attribute to make it the clickable target.

{% highlight html linenos %}
<div data-whisk-widget
    data-whisk-product-text="Dill pickles"
    class="demo_widget_wrapper">
  This Widget let's you
  <a data-whisk-action="view_list" class="demo_widget green">
    View your Whisk Shopping List
  </a>
  <br>
  but let's face it - you really want to
  <a data-whisk-action="add_product_to_list" class="demo_widget brown">
    <i class="fa fa-check-square"></i> Add Dill pickles
  </a>
</div>
{% endhighlight %}

Which looks like:

<div data-whisk-widget
    data-whisk-product-text="Dill pickles"
    class="demo_widget_wrapper">
  This Widget let's you
  <a data-whisk-action="view_list" class="demo_widget green">
    View your Whisk Shopping List
  </a>
  <br>
  but let's face it - you really want to
  <a data-whisk-action="add_product_to_list" class="demo_widget brown">
    <i class="fa fa-check-square"></i> Add Dill pickles
  </a>
</div>



# Adding your own internal product identifiers

While WhiskConncect works primarily with product text, you may care to add and track specific products, with unique internal identifiers. For this reason, you can associate a Product ID with each WhiskConnected product.

Consider the following example, where a salt manufacturer sells three different types of salt, but would rather keep things simple for the user by just adding "Salt" to the Whisk Shopping List:

<table>
  <thead>
    <tr><th>Product</th><th>ID</th><th>Product Text</th></tr>
  </thead>
  <tbody>
    <tr><td>1kg Extra value salt</td><td><code>salt-1</code></td><td>Salt</td></tr>
    <tr><td>500g Everyday salt</td><td><code>salt-2</code></td><td>Salt</td></tr>
    <tr><td>100g Premium salt</td><td><code>salt-3</code></td><td>Salt</td></tr>
  </tbody>
</table>

This is easy to achieve in WhiskConnect: each widget just needs to identify the product ID and text, we'll automatically separate tracking and analytics, and you'll be able to see which prodcut drives higher conversion.

## Add a product ID to a widget

To add a product ID to a widget, you simply need add the `data-whisk-owner-product-id="<your ID here>"` to the widget element:

{% highlight html linenos %}
<div style="margin: 1ex; padding: 1ex;">
  Choose your salt:
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-1"
      data-whisk-product-text="Salt">
    1kg Extra value salt
  </button>
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-2"
      data-whisk-product-text="Salt">
    500g Everyday salt
  </button>
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-3"
      data-whisk-product-text="Salt">
    100g Premium salt
  </button>
</div>
{% endhighlight %}

which would produce the following buttons:

<div style="margin: 1ex; padding: 1ex;">
  Choose your salt:
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-1"
      data-whisk-product-text="Salt">
    1kg Extra value salt
  </button>
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-2"
      data-whisk-product-text="Salt">
    500g Everyday salt
  </button>
  <button type="button"
      data-whisk-widget
      data-whisk-owner-product-id="salt-3"
      data-whisk-product-text="Salt">
    100g Premium salt
  </button>
</div>

Of course, this example is a little contrived - but it shows how it is possible for different product-text values to be associated with the same product ID, and vice-versa.


# Using WhiskConnect in non-English languages

By default, WhiskConnect assumes your products are written in English, but we at Whisk love all languages... we're just a bit time-limited.

We support a number of other languages, and you can specify the language of a product widget by including the `data-whisk-language` attribute, and specifying a language code. Here are a few examples:

The list of supported languages at present is:

<table>
  <thead>
    <tr><th>Language</th><th>Code</th></tr>
  </thead>
  <tbody>
    <tr><td>English</td><td><code>en</code></td></tr>
    <tr><td>English (GB)</td><td><code>en-gb</code></td></tr>
    <tr><td>English (US)</td><td><code>en-us</code></td></tr>
    <tr><td>French</td><td><code>fr</code></td></tr>
    <tr><td>French (Quebec)</td><td><code>fr-qc</code></td></tr>
    <tr><td>German</td><td><code>de</code></td></tr>
    <tr><td>Polish</td><td><code>pl</code></td></tr>
    <tr><td>Spanish</td><td><code>es</code></td></tr>
    <tr><td>Spanish (Argentinian)</td><td><code>es-ar</code></td></tr>
    <tr><td>Spanish (Mexican)</td><td><code>es-mx</code></td></tr>
  </tbody>
</table>

## Setting your language with a `<meta>` tag

If you wish to set your language across all widgets on the page, the easiest way to do this is by adding a `<meta>` tag:

{% highlight html %}
<meta name="whisk-language" content="fr">
{% endhighlight %}

All widgets will pick up this language correctly.

## Setting your language with a data-attribute

Alternatively, if you'd rather set the language on each widget, you can do so with a data-attribute.

Here's our original button, but this time for a French product:

{% highlight html linenos %}
<button type="button"
    data-whisk-widget
    data-whisk-language="fr"
    data-whisk-product-text="Escargot">
  Ajouter "Escargot" à votre liste de courses
</button>
{% endhighlight %}

and here's how it looks in action:

<button type="button"
    data-whisk-widget
    data-whisk-language="fr"
    data-whisk-product-text="Escargot">
  Ajouter "Escargot" à votre liste de courses
</button>



# Automatically open WhiskConnect for display ads

One of the key benefits of WhiskConnect is that you can use it to enable product purchase across all of your advertising channels. For instance, you might have a product page on your website, and then drive traffic to that page with the usual advertising strategies - display advertising on other sites, YouTube ads, Facebook ads, Social media promotions, etc.

Here's a quick demo of how WhiskConnect works for a simple display advertising setup. Imagine you took out a banner advert to advertise your product "Whisk Wonder Salt". It'd probably look something like this:

<div id="fake_page">
  <a id="banner_advert" href="/connect/demo_salt/?whisk_medium=DisplayAd&whisk-show=1&whisk_source=WhiskDevDocs&whisk_content=ProductLink&whisk_campaign=WhiskDevDemos&whisk_term=Salt">
    <img src="/connect/images/salt_product.png" alt="Salt" width="100">
    Whisk Wonder Salt!
  </a>
  <div id="fake_site_content"></div>
</div>

The display advert links to a our own fake product page, but the URL is special:

{% highlight html %}
http://whisklabs.github.io/connect/demo_salt/?whisk_medium=DisplayAd&whisk-show=1&whisk_source=WhiskDevDocs&whisk_content=ProductLink&whisk_campaign=WhiskDevDemos&whisk_term=Salt
{% endhighlight %}

This URL has been generated using the [WhiskConnect URL Generator](https://connect.whisk.com/#!/utils/urlgenerator), which adds campaign tracking information to the URL, so that WhiskConnect will correctly add products to the list and track their origin.  Please see the URL generator pages for details on how to create your own campaign URLs.

WhiskConnect generated URLs can be used across all your existing advertising and social platforms - wherever you'd normally send people to a product, you can use WhiskConnect to enable that product for the Whisk Shopping List.


# Having trouble?

[Get in touch](mailto:tech@whisk.co.uk) and we'll do our best to help!


<style>

  .demo_widget_wrapper {
    border-radius: 5px;
    border: 1px solid #777;
    color: #333;
    background-color: #ddd;
    padding: 1em;
  }
  .demo_widget {
    display: inline-block;
    padding: 1ex;
    margin: 1ex;
    border-radius: 5px;
    border: 1px solid #777;
    cursor: pointer;
  }
  .red {
    color: white;
    background-color: red;
  }
  .green {
    color: white;
    background-color: green;
  }
  .brown {
    color: white;
    background-color: #930;
  }

  #fake_page {
    border: 5px solid #777;
    border-radius: 5px;
    background: white;
  }

  #fake_page #banner_advert {
    display: block;
    width: 100%;
    font-size: 28px;
    padding: 1em;
    margin: 1em;
  }
  #fake_page #fake_site_content {
    width: 100%;
    height: 400px;
    background: url("{{ baseurl }}/connect/images/fake_wikipedia.png");
  }
</style>

<meta name="whisk-owner-id" content="d84ecba1-bfb1-4395-99f0-ae02910d4802">

<script async="true" src="//widget.whisk.com/assets/whiskbutton.js" type="text/javascript"></script>
