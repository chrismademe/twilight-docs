---
title: "Javascript and CSS"
eleventyNavigation:
  key: "Javascript and CSS"
  parent: "Syntax"
  order: 5
---

Twilight isn't very opinionated when it comes to Javascript or CSS, however you can write these directly inside your components using the special `Style` and `Script` components. These will be extracted and saved as a `css` and `js` files.

```html
<a :href="href" class="btn">
    <Children />
</a>

<Style>
    .btn {
        background: blue;
        color: white;
    }
</Style>

<Script>
    console.log('Hello from the button');
</Script>
```

These will be saved in the `assets` directory, which can be set on the Compiler.

```txt
assets/
    components/
        Button/
            style.css
            script.js
```