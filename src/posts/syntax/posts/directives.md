---
title: "Directives"
eleventyNavigation:
  key: "Directives"
  parent: "Syntax"
  order: 2
---

## Directives

Directives are special attributes that instruct the compiler to do something with the output of an element. Commonly this is wrapping the markup with some Twig syntax, like an if conditional. Directives always start with an @ symbol.

## @if
Wraps an element in an if condition

```html
<p @if="someCondition">
    I will only show up is someCondition is true
</p>
```

{% include "partials/arrow.html" %}

```html
{% verbatim %}{% if someCondition %}
    <p>
        I will only show up is someCondition is true
    </p>
{% endif %}{% endverbatim %}
```

## @unless
Wraps an element in an if condition, checking for a falsey value

```html
<p @unless="someCondition">
    I will only show up is someCondition is false
</p>
```

{% include "partials/arrow.html" %}

```html
{% verbatim %}{% if not someCondition %}
    <p>
        I will only show up is someCondition is true
    </p>
{% endif %}{% endverbatim %}
```

## @for

Wraps an element in a for loop. You may also use `@each`, if you prefer.

```html
<ul>
	<li @for="post in posts">{% verbatim %}{{ post.title }}{% endverbatim %}</li>
</ul>
```

{% include "partials/arrow.html" %}

```html
<ul>
    {% verbatim %}{% for post in posts %}
        <li>{{ post.title }}</li>
    {% endfor %}{% endverbatim %}
</ul>
```

## @checked

Will add a `checked` attribute to a Checkbox input if the passed value is true.

```html
<input
    type="checkbox"
    name="isComplete"
    @checked="task.isComplete"
/>
```

{% include "partials/arrow.html" %}

```html
<input
    type="checkbox"
    name="isComplete"
    {% verbatim %}{{ task.isComplete ? 'checked' : '' }}{% endverbatim %}
/>
```

## @disabled

Will add a `disabled` attribute to an element if the passed value is true.

```html
<input
    type="checkbox"
    name="isComplete"
    @disabled="task.isComplete"
/>
```

{% include "partials/arrow.html" %}

```html
<input
    type="checkbox"
    name="isComplete"
    {% verbatim %}{{ task.isComplete ? 'disabled' : '' }}{% endverbatim %}
/>
```

## @selected

Will add a `selected` attribute to an element (usually an `<option>`) if the expression passed matches that of the `value` attribute, for example if `user.country` is "UK", the UK option will be selected.

```html
<select name="country">
    <option value="UK" @selected="user.country">United Kingdom</option>
    <option value="US" @selected="user.country">United States</option>
</select>
```

{% include "partials/arrow.html" %}

```html
<select name="country">
    <option value="UK" {% verbatim %}{{ user.county == "UK" ? 'selected' : '' }}{% endverbatim %}>United Kingdom</option>
    <option value="US" {% verbatim %}{{ user.county == "US" ? 'selected' : '' }}{% endverbatim %}>United States</option>
</select>
```

## @text

Inserts the content of a variable inside the element, with HTML escaped.

```html
<span @text="post.author" />
```

{% include "partials/arrow.html" %}

```html
{% verbatim %}<span>{{ post.author }}</span>{% endverbatim %}
```

## @html

Inserts the content of a variable inside the element, with the `raw` filtered applied

```html
<datetime @html="post.date()" />
```

{% include "partials/arrow.html" %}

```html
{% verbatim %}<datetime>{{ post.date() | raw }}</datetime>{% endverbatim %}
```

## @attributes

Adds a collection of attributes to the current element. Can be a simple string of attributes or an array with key, value pairs. You may omit a value for this directive, and it will assume the variable name is `attributes`

```html
<div @attributes /> <!-- The same as @attributes="attributes" -->
```