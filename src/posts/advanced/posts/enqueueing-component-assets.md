---
title: "Enqueueing Component Assets"
eleventyNavigation:
  key: "Enqueueing Component Assets"
  parent: "Advanced"
  order: 3
---

This pages examples are specific to WordPress, but you can use the same concept in other Frameworks.

Twilight allows you to write Javascript and CSS in your template. It then extracts them and creates a file in your specified output directory. In WordPress, to enqueue them, you can do this:

```php
add_action( 'wp_enqueue_scripts', 'theme_enqueue_component_assets' );

function theme_enqueue_component_assets() {
  $css = glob( get_template_directory() . '/assets/**/**/*.css' );
  $js = glob( get_template_directory() . '/assets/**/**/*.js' );

  if ( ! empty($css) ) {
    foreach ($css as $path) {
      $path = str_replace( get_template_directory(), get_template_directory_uri(), $path );
      $name = basename( rtrim($path, 'style.css') );
      wp_enqueue_style( $name, $path );
    }
  }

  if ( ! empty($js) ) {
    foreach ($js as $path) {
      $path = str_replace( get_template_directory(), get_template_directory_uri(), $path );
      $name = basename( rtrim($path, 'script.js') );
      wp_enqueue_script( $name, $path );
    }
  }
}
```