---
title: "Caching Compiled Views"
eleventyNavigation:
  key: "Caching Compiled Views"
  parent: "Advanced"
  order: 1
---

While Twilight is pretty fast, in production, you don't need to compile your views on every request. To stop this, simply pass a boolean value to the `if` argument of the `compile` function.

In WordPress, you can use the `wp_get_environment_type` function:

```php
<?php

use Twilight\Twilight;

Twilight::compile(
    input: get_template_directory() . '/views',
    output: WP_CONTENT_DIR . '/.views',
    assets: get_template_directory() . '/assets',
    if: wp_get_environment_type() === 'local'
);
```

In Laravel, you could use the `env()` helper:

```php
<?php

use Twilight\Twilight;

Twilight::compile(
    input: 'resources/views',
    output: 'storage/app/views',
    assets: 'public/assets',
    if: env('APP_ENV') === 'development'
);
```