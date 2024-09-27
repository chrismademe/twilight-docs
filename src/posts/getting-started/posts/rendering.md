---
title: "Rendering"
summary: "We use eleventy --serve and compile Sass with sass-cli with npm scripts."
eleventyNavigation:
  key: Rendering
  parent: "Getting Started"
  order: 2
---

The first step before rendering views is to setup the compiler.

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

**Important Note:** You should not place the compiler inside a conditional. This method is responsible for setting up the Twig environment. To conditionally prevent compilation, pass a boolean value to the `if` argument.

Now, assuming your theme is a Classic or Hybrid theme, you can render a view from a template file. The below example uses the homepage template (`front-page.php`), passing the current page object to the template.

```php
<?php

use function Twilight\Twilight;

Twilight::render(
    template: 'home.twig',
    context: [
        'page' => get_post()
    ]
);
```

## Rendering in ACF Blocks

This section assumes you're familiar with ACF Blocks and how to register them, you can <a href="https://www.advancedcustomfields.com/resources/blocks/">read more about that on their site</a>.

To render Twilight from an ACF Block, you'll first need to create a render function that you can use with ACF. Below is an example:

```php
<?php

use Twilight\render;

/**
 * @param array $block The block settings and attributes.
 * @param string $content The block inner HTML (empty).
 * @param bool $is_preview True during AJAX preview (in the editor)
 * @param (int|string) $post_id The post ID this block is saved to.
 */
function render_acf_block(
    array $block,
    string $content,
    bool $is_preview,
    int|string $post_id
) {
    $context = [
        'block' => $block,
        'post_id' => $post_id,
        'fields' => get_fields()
        'is_preview' => $is_preview,
        'attributes' => $is_preview ? '' : get_block_wrapper_attributes(),
    ];

    $template = sprintf( 'blocks/%s/template.twig', $block['name'] );

    /**
     * Filter context, this allows you to manipulate the context
     * of a block (or all blocks) before render
     */
    $context = apply_filters( 'block', $context );
    $context = apply_filters( sprintf( 'block.%s', $block['name'] ), $context );

    return render(
        template: $template,
        context: $context
    );
}
```

Now, specify the render callback in your block.json:

```json
"acf": {
    "renderCallback": "render_acf_block"
}
```
