---
title: "Component Structure"
eleventyNavigation:
  key: "Component Structure"
  parent: "Components"
  order: 0
---

Components live in the `components/` directory, which should be directly inside your `views/` directory.

```txt
views/
    components/
        ComponentName/
            component.php
            template.twig
```

The only required file is `template.twig`, which should contain the markup for your component. You may use the `component.php` file to run PHP code associated with your component. You can read more about that in <a href="/components/passing-data-to-components/">Passing Data to Components</a>