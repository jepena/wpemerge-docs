# Sprites

## SVG Sprite

Adding images inside the `resources/images/sprite-svg/` directory will combine them into a single sprite file.
The sprite file will be automatically output in your site's footer so SVGs don't block loading critical site content.

To output a single SVG from the sprite you have to use an SVG reference:
```html
<svg><use xlink:href="#my-sprite-id" /></svg>
```

In the example above, `my-sprite-id` represents the filename for the original SVG file, without the extension. Here are a couple more examples:

| File | SVG |
| --- | --- |
| `resources/images/sprite-svg/home.svg` | `<svg><use xlink:href="#home" /></svg>` |
| `resources/images/sprite-svg/github.svg` | `<svg><use xlink:href="#github" /></svg>` |
| `resources/images/sprite-svg/heart-icon.svg` | `<svg><use xlink:href="#heart-icon" /></svg>` |

## Raster Sprite
Adding images inside the `resources/images/sprite/` directory will combine them into a single sprite file. To use a sprite image in your styles you can employ one of the automatically generated SASS mixins in `resources/styles/_sprite.scss`.
In addition, a variable will be automatically defined for every sprite image you add - these variables can be used as a reference in mixins (e.g. `birds.jpg` becomes `$birds`).

!> `resources/styles/_sprite.scss` is an automatically generated file - never modify it manually.

### Examples
1. Add a sprite image as a background:
    ```scss
    .foo {
        @include sprite-image($birds);
    }
    ```

2. Add a sprite image as a background and set the element's width and height to the exact dimensions of the image:
    ```scss
    .foo {
        @include sprite($birds);
    }
    ```

3. Set an element's height to be equal to a sprite image's height:
    ```scss
    .foo {
        @include sprite-height($birds);
    }
    ```

Refer to the generated comments inside `resources/styles/_sprite.scss` for more information and examples.

### Retina Support

To enable retina support for sprites follow these steps:

1. Edit `resources/build/webpack.js` and uncomment the following line:
    ```js
    // retina: '@2x',
    ```
2. Restart the dev process if you have it running.
3. For every image you have in `resources/images/sprite/`, create a retina copy with `@2x` added as a suffix to the filename (e.g. `foo.jpg` should have a `foo@2x.jpg` retina version).
4. Replace mixin usage with the appropriate retina counterpart and add a `-group` suffix to your sprite variable (e.g. `@include sprite($birds);` becomes `@include retina-sprite($birds-group);`)

That's it! Completing the above steps ensures the build process will add relevant media queries to replace the sprite image references with the retina version for suitable devices.

If you wish to read more on how sprites work and how to use them check out the following:
- https://github.com/Ensighten/spritesmith
- https://github.com/twolfson/spritesheet-templates
- https://github.com/mixtur/webpack-spritesmith
