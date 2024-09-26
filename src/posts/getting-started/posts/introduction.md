---
title: "Introduction"
summary: "Welcome to the official documentation of Spruce Docs Elventy theme. A small template that you can use to document any of your projects."
eleventyNavigation:
  key: Introduction
  parent: "Getting Started"
  order: 1
---

## Installation

Twilight allows you to build PHP/WordPress sites in a component-based way.
Twilight requires PHP version 8.2 or higher. To get started, install it with Composer:

```bash
composer require chrismademe/twilight
```

## What Is It?

If you're familiar with building templates in Twig, or even WordPress - you'll know that one of the big things that it doesn't really allow for it components. In Twig, you might do something like this:

```html
{% verbatim %}
{% set content %}
  <h1>WordPress Website Development</h1>
  <p>Expert WordPress Development services in London</p>
{% endset %}

{% include "partials/hero.twig" with { image: '/images/hero.jpg', content: content } %}
{% endverbatim %}
```

This is fine, but it doesn't "feel" like HTML. And what if you want to manipulate or do something with that incoming data on the component side?

Twilight adds a Component syntax to Twig, so you can do this:

```html
<Hero image="/images/hero.jpg">
  <h1>WordPress Website Development</h1>
  <p>Expert WordPress Development services in London</p>
</Hero>
```

But that's all, have a read through the docs to learn about <a href="/components/passing-data-to-components/">passing data to components</a>, manipulating that data and the handy <a href="/syntax/directives/">directives</a> that you can use in your templates.