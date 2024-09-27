---
title: "Modifying the Twig Environment"
eleventyNavigation:
  key: "Modifying the Twig Environment"
  parent: "Advanced"
  order: 2
---

Twig offers a variety of options that you can pass to the Environment, to do this with Twilight, you may hook into the `twig:init` event and modify the instance. Here's an example of adding a custom Twig function:

```php
<?php

use Twig\TwigFunction;
use Twig\Environment;
use Twilight\Events;

Events::on( 'twig:init', function( Environment $twig ) {
    $twig->addFunction( new TwigFunction( 'do_a_thing', 'do_a_thing' ) );
} );

```