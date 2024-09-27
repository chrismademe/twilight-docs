---
title: "Defining a Prop Schema"
eleventyNavigation:
  key: "Defining a Prop Schema"
  parent: "Components"
  order: 2
---

You can pass data to components without first defining them, however it's often useful to validate props or provide default values. To do this, you can use the `schema` method when registering a component.

```php
<?php

use Twilight\Component;

Component::name('Button')
    ->schema( [
        'href' => [
            'type' => 'string'
        ],
        'size' => [
            'type' => 'enum',
            'values' => ['sm', 'md','lg'],
            'default' => 'md'
        ],
        'type' => [
            'type' => 'enum',
            'values' => ['button', 'submit', 'reset']
        ]
    ] )
    ->register();

```

## Prop Types

When defining a prop schema, there are various types you can choose from.

- `string`
- `int`
- `number`
- `array`
- `enum`
- `bool`/`boolean`
- `float`
- `object`
- `callable`
- `instanceof`

During validation, if a prop fails, a `Twilight\Exception\InvalidPropException` will be thrown.

### Schema array

Each prop type supports the following keys:

- `type` - The prop type (from the list above)
- `required` - Boolean value, whether the prop is required
- `default` - Default value if no value is set for this prop

The `enum` type also supports `value`, which should be an array of accepted values.

The `instanceof` type also accepts an `instanceof` key, which should be the class you want to check against.

## Custom Prop Validaton

In cases where you need to do more complex checks, you may pass in a callback using the `validator` key. The callback receives the prop value, name and an array of props and should return `false` if the value is considered invalid.

```php
<?php

use Twilight\Component;

Component::name('PostCard')
    ->schema( [
        'post' => [
            'validator' => function( $value, $name, $props ) {
                // Prop must be a Post object of a Post ID
                return $value instanceof WP_Post::class
                    || is_int($value);
            }
        ]
    ] )
    ->data( function( $data ) {
        if ( is_int( $data['post'] ) ) {
            $data['post'] = get_post( $data['post'] );
        }
        return $data;
    } )
    ->register();
```