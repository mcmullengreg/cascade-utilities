+++
title = "SVG Sprite"
description = ""
weight = 1

+++

{{< lead >}}
This script helps take a folder of SVG files and combines them into a single SVG, to be used as a Sprite. The files can live anywhere on your site. In this example we are also using a default object called `$framework` to pull in the location of the framework site and/or folder.
{{< /lead >}}

## Sample Structure

```shell
Site://Name
│
└───images
│   └───icons
│       │   file.svg
│       │   file2.svg
│       │   ...
│
└───formats
    └───svg-sprite.vm
```

## Usage
Setup your template to utilize this format as a region, or import it as you see fit. The first variable finds the location of the SVGs to build out the sprite. Set your default site as you see fit.

```html
#set ( $icons = $_.locateFolder("/path-to/svgs", $svgSite) )
```

We then loop through the children and utilize the `#cleanSVG()` macro to clean the SVG items, customize as you see fit, ensuring we keep the viewBox while swapping the `svg` element for `symbol`.

At the moment, SVG's should be placed into your Cascade CMS instance _without_ comments. Comments are not filtered out, but could be added to the list in your installation.

ID's of the SVG sprite are based on the assets `.label`, lcased. Filenames are not stripped if Display Name or Title are not used. Therefore the default name could be `icon-name-svg`.

### Example SVG

```html
<svg xmlns="***" viewBox="***" ...>
  <path|group|etc>
</svg>
```

## Using the Sprite

To use the sprite, you'll use the `<use xlink:href="#icon-name"></use>`. Cascade CMS doesn't like this code, so make sure to wrap it with a `#protect`.

```html
<svg class="whatever">
  <!--#protect<use xlink:href="#icon-name"></use>#protect-->
</svg>
```

## Resources

* [A Pretty Good SVG Icon System](https://css-tricks.com/pretty-good-svg-icon-system/)
* [Inline SVG...Cached](https://css-tricks.com/inline-svg-cached/)
* [Why Inline SVG is Best SVG](https://css-tricks.com/inline-svg-best-svg/)
* [How to Use SVG Image Sprites](https://www.sitepoint.com/use-svg-image-sprites/)
* [5 Gotchas You're Gonna Face Getting Inline SVG Into Production](https://css-tricks.com/gotchas-on-getting-svg-into-production/)
